<h1 style="text-align: start;">executeSql 函數 step by step, 第 15 章，Join 子句</h1><h4 style="text-align: start;"><span style="color: var(--color); background-color: var(--background);">executeSql 只支援 Inner Join 和 Left Join，不支援 Full Join 和 Right Join</span></h4><pre><code >Select searchFields( anyfields on talbleLeft or talbeRight ) 
From tableLeft[ Inner | Left ] 
Join tableRight On tableLeft.keyField = tableRight.keyField</code></pre><h3 style="text-align: start;">Inner join：</h3><p style="text-align: start;">為內部合併查詢指令，可以取回2個資料表都共同存在合併欄位的記錄資料。也就是在「兩個資料表都有在 on 關鍵字所指定的欄位的值」這個條件下才取出想取的欄位。<br>Inner join 也可以只寫 join</p><h3 style="text-align: start;">Left Join：</h3><p style="text-align: start;">左外部合併查訊，是在合併兩個資料表中，取回左邊資料表的所有紀錄，就算在右邊資料表沒有存在合併欄位的值，顯示結果會以左邊資料表為主。</p><h3 style="text-align: start;">範例：1</h3><pre><code >let (
[
~queryFake ="  Select company::name, contact::name, contact::nameEng, contact::addrCity, contact::addrStr 
From contact   
Join company On contact::idf = company::id   
Where contact::addrCity = ? 
Order By contact::addrStr, contact::name " ;
~query = substitute ( ~queryFake ; "::" ; "." )
/* 被轉換成,
Select company.name, contact.name, contact.nameEng, contact.addrCity, contact.addrStr  From contact    Join company On contact.idf = company.id    Where contact.addrCity = ?  Order By contact.addrStr, contact.name 
*/
];
ExecuteSql ( ~query ; "" ; "" ; "台東縣" ))</code></pre><p>在 contact 表中沒有公司名稱，而是指定 <span style="color: rgb(0, 0, 0);">Join company On contact::idf = company::id ，透過這個指定，把 company.name 引進來。</span></p><p><span style="color: rgb(0, 0, 0);">這是 Inner Join 只有在 Join company On contact::idf = company::id 這個條件成立的資料才會被傳回。</span></p><h3><span style="color: rgb(0, 0, 0);">範例：2</span></h3><pre><code >let (~query ="  
Select name, name, nameEng, addrCity, addrStr 
From contact   
Join company On idf = id   
Where addrCity = ? 
Order By addrStr, name " ;
ExecuteSql ( ~query ; "" ; "" ; "台東縣" ))</code></pre><p>這是會發生錯誤的寫法</p><p>會出現如: </p><p>The column named "name" appears in more than one table in the column reference's scope.</p><p>如果兩張表裡有相同的欄位名稱，在敘述中被引用，必須加以完全表示，如範例：1</p><p>有關於 debug 請參考第 14 章</p><h3>範例：3</h3><pre><code >let (
[
~queryFake ="  Select company::name, contact::name, contact::nameEng, contact::addrCity, contact::addrStr 
From contact   
Left Join company On contact::idf = company::id   
Where contact::addrCity = ? 
Order By contact::addrStr, contact::name " ;
~query = substitute ( ~queryFake ; "::" ; "." )
/* 被轉換成,
Select company.name, contact.name, contact.nameEng, contact.addrCity, contact.addrStr  From contact    Join company On contact.idf = company.id    Where contact.addrCity = ?  Order By contact.addrStr, contact.name 
*/
];
ExecuteSql ( ~query ; "" ; "" ; "台東縣" ))</code></pre><p><span style="color: rgb(0, 0, 0);">這是 Left Join，Left Table 只要符合 Where 子句的條件就會被傳回， 不一定要符合 Join company On contact::idf = company::id 這個條件。</span></p>