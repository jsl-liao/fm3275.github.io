<h2><span style="color: rgb(0, 0, 0);">executeSql 函數 step by step, 第 29 章，關係運算子_Between</span></h2><p style="text-align: start;"><strong>Between</strong> 則是用來限定依某範圍內連續的值作為條件來搜尋資料表中的特定資料。</p><p style="text-align: start;">作為查詢範圍條件的欄位型態可為數值、日期或字串，其中字串是依照字母排列順序來界定範圍。</p><p style="text-align: start;"><strong>Not Between</strong> 是 <strong>Between</strong> 的否定形式。</p><h3 style="text-align: start;">範例 1：</h3><pre><code >ExecuteSQL ( "
Select company.name, company.addrCity, contact.name, contact.nameEng 
From contact 
Join company On contact.idf = company.id 
Where company.addrCity = '新北市' And contact.stroke Between 20 And 22
"; Char(9) ; "" )</code></pre><p>找出公司地址在新北市，姓的筆畫數在 20 到 22 劃之間的人。</p><h3><span style="color: rgb(0, 0, 0);">範例 2：</span></h3><pre><code >ExecuteSQL ( "
Select company.name, company.addrCity, contact.name, contact.nameEng 
From contact 
Join company On contact.idf = company.id 
Where company.addrCity = '新北市' And contact.nameEng Between 'A' And 'F' And contact.stroke Between 20 And 22
"; Char(9) ; "" )</code></pre><p><span style="color: rgb(0, 0, 0);">找出公司地址在新北市，姓的筆畫數在 20 到 22 劃之間，而且英文名字是以 A ~ E 開頭的人（英文名字沒有單一個 F 的人）。</span></p><p><span style="color: rgb(0, 0, 0);">為了能夠更容易閱讀和理解，可以用括號把條件區隔開，把計算式寫成如下：</span></p><pre><code >ExecuteSQL ( "
Select company.name, company.addrCity, contact.name, contact.nameEng 
From contact 
Join company On contact.idf = company.id 
Where ( company.addrCity = '新北市' ) And ( contact.nameEng Between 'A' And 'F' ) And ( contact.stroke Between 20 And 22 )
"; Char(9) ; "" )</code></pre><p><br></p>