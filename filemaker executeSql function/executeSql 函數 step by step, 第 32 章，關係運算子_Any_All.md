<h2 style="text-align: start;"><span style="color: rgb(0, 0, 0);">executeSql 函數 step by step, 第 32 章，關係運算子_Any_All</span></h2><p>將值與子查詢返回的每個值進行比較（ <strong>Any</strong> 的前面必須是 =、&lt;&gt;、&gt;、&gt;=、&lt; 或 &lt;=），只要符合其中之一便可。</p><p><span style="color: rgb(33, 37, 41); background-color: rgb(250, 250, 250); font-size: 16px;"><strong>= Any</strong></span><span style="color: rgb(33, 37, 41); background-color: rgb(250, 250, 250); font-size: 16px;"> 相當於 </span><span style="color: rgb(33, 37, 41); background-color: rgb(250, 250, 250); font-size: 16px;"><strong>In</strong></span></p><p><span style="color: rgb(33, 37, 41); background-color: rgb(250, 250, 250); font-size: 16px;"><strong>Any 和 All 的語法是相同的。</strong></span></p><p><span style="color: rgb(33, 37, 41); background-color: rgb(250, 250, 250); font-size: 16px;"><strong>Any 是符合子查詢其中的任何一項就取值。</strong></span></p><p><span style="color: rgb(33, 37, 41); background-color: rgb(250, 250, 250); font-size: 16px;"><strong>All 則必須是符合所有</strong></span><span style="color: rgb(0, 0, 0);">符合子查詢的任何一項才取值。</span></p><h3><span style="color: rgb(33, 37, 41); background-color: rgb(250, 250, 250); font-size: 16px;"><strong>範例 1：</strong></span></h3><p><span style="color: rgb(33, 37, 41); background-color: rgb(250, 250, 250); font-size: 16px;">第30章的範例 2 可以改寫為</span></p><pre><code >executeSql ("Select name, nameEng, gender From contact Where idf = Any
( Select id From company Where addrCity = '新北市' And name like '%材料科技股份有限公司' )"; ",  " ; "")</code></pre><h3><span style="color: rgb(0, 0, 0);">範例 2：</span></h3><p>轉機事材料科技有限公司的員工只要比二路玩工業有限公司其中任何一個人的年紀大，就列出</p><p>有三種寫法都可以獲得正確的資料，但是執行效率有差別，你可以比較看看。</p><p>第 1 種寫法:</p><pre><code >ExecuteSQL ( "
Select y.name, t.name, t.nameEng, t.age 
From contact t 
Join company y On t.idf = y.id 
Where y.name = '轉機事材料科技有限公司' And t.age &gt; Any (
Select ct.age 
From contact ct 
Join company cy On ct.idf = cy.id 
Where cy.name = '二路玩工業有限公司')
"; "" ; "")</code></pre><p><span style="color: rgb(0, 0, 0);">第 2 種寫法:</span></p><pre><code >ExecuteSQL ( "
Select y.name, t.name, t.nameEng, t.age 
From contact t 
Join company y On t.idf = y.id 
Where y.name = '轉機事材料科技有限公司' And t.age &gt; Any (
Select c.age 
From contact c 
Join company cy On c.idf = cy.id 
Where cy.name = '二路玩工業有限公司')
"; "" ; "")</code></pre><p><span style="color: rgb(0, 0, 0);">第 3 種寫法:</span></p><p><span style="color: rgb(0, 0, 0);">cf_listToAnother 可以在 custom function 的 folder 中找到 </span></p><pre><code >let ([
~inVl = executeSql("
Select c.age 
From contact c 
Join company cy On c.idf = cy.id 
Where cy.name = '二路玩工業有限公司'
" ; "" ; "");
~inStr = cf_listToAnother ( ~inVl ; "sqlIn" ; "num")];  
ExecuteSQL("
Select y.name, t.name, t.nameEng, t.age 
From contact t 
Join company y On t.idf = y.id 
Where y.name = '轉機事材料科技有限公司' And t.age &gt; Any ( " & ~inStr &"    )
" ; "" ; "" ))</code></pre><p>錯誤的寫法</p><pre><code >ExecuteSQL("
Select company.name, contact.name, contact.nameEng, contact.age 
From contact 
Join company On contact.idf = company.id 
Where company.name = '轉機事材料科技有限公司' And contact.age &gt; Any (
Select contact.age 
From contact 
Where company.name = '二路玩工業有限公司')
"; "" ; "")</code></pre><p>原因：Join 子句在<span style="color: rgb(0, 0, 0);">每一個 Select 敘述中都必須獨立的存在，不同的 Select 敘述不能共用 Join 子句。</span></p>