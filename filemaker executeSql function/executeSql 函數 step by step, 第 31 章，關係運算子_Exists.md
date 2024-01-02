<h2><span style="color: rgb(0, 0, 0);">executeSql 函數 step by step, 第 31 章，關係運算子_Exists</span></h2><p><span style="color: rgb(0, 0, 0);">EXISTS 運算子可以連接</span><a href="https://www.fooish.com/sql/subquery.html" target="" style="text-align: start;">子查詢</a><span style="color: rgb(0, 0, 0);">，用來判斷子查詢是否有返回的結果，如果有結果返回則為真、否則為假。</span></p><p><span style="color: rgb(0, 0, 0);">若 EXISTS 為真，就會繼續執行外查詢中的 SQL；</span></p><p><span style="color: rgb(0, 0, 0);">若 EXISTS 為假，則整個 SQL 查詢就不會返回任何結果。</span></p><h3><span style="color: rgb(0, 0, 0);">範例：</span></h3><p><span style="color: rgb(0, 0, 0);">和第 30 章的範例 2 取得相同的結果。</span></p><pre><code >executeSql ("
Select contact.name, contact.nameEng, contact.gender 
From contact 
Where Exists ( 
  Select id From company 
  Where contact.idf = company.id And (addrCity = '新北市') And (name like '%材料科技股份有限公司'))
"; ",  " ; "")</code></pre><p>雖然可以取得相同的結果，但是執行的速度慢很多。通常，愈複雜的計算式，越耗時。</p><p>這就是一個例子。</p>