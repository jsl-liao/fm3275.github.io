<h2><span style="color: rgb(0, 0, 0);">executeSql 函數 step by step, 第 13 章，Select 敘述的安全寫法</span></h2><h3>作法</h3><ol><li>在 data viewer 輸入 Select 敘述，欄位名稱使用完全限定名稱（ fully qualified name , tableName::fieldName ）</li><li>把 “::" 置換成 “.“，轉換成 executeSql 合法敘述。</li><li><span style="color: rgb(0, 0, 0);">應用於 Join 子句的狀況下，不同表的取值的欄位如果有相同名稱必須加表的標示，否則會發生錯誤。</span></li><li><span style="color: rgb(0, 0, 0);">這個方法好用之處在於：在 data viewer 左邊的欄位區域雙擊欄位變可以取得完全限定名稱，避免手動輸入的錯誤。</span></li><li><span style="color: rgb(0, 0, 0);">如果 executeSql 只對一個表取值，也可以應用。</span></li></ol><h3><span style="color: rgb(0, 0, 0);">範例：</span></h3><pre><code >let (
[
~queryFake ="  
Select company::name, contact::name, contact::nameEng, contact::addrCity, contact::addrStr 
From contact   
Join company On contact::idf = company::id   
Where contact::addrCity = ? 
Order By contact::addrStr, contact::name " ;
~query = substitute ( ~queryFake ; "::" ; "." )
];
ExecuteSql ( ~query ; "" ; "" ; "台東縣" ))</code></pre><p><br></p>