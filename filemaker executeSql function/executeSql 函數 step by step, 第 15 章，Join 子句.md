executeSql 函數 step by step, 第 15 章，Join 子句
==========================================

#### executeSql 只支援 Inner Join 和 Left Join，不支援 Full Join 和 Right Join

    Select searchFields( anyfields on talbleLeft or talbeRight ) 
    From tableLeft[ Inner | Left ] 
    Join tableRight On tableLeft.keyField = tableRight.keyField

### Inner join：

為內部合併查詢指令，可以取回2個資料表都共同存在合併欄位的記錄資料。也就是在「兩個資料表都有在 on 關鍵字所指定的欄位的值」這個條件下才取出想取的欄位。  
Inner join 也可以只寫 join

### Left Join：

左外部合併查訊，是在合併兩個資料表中，取回左邊資料表的所有紀錄，就算在右邊資料表沒有存在合併欄位的值，顯示結果會以左邊資料表為主。

### 範例：1

    let (
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
    ExecuteSql ( ~query ; "" ; "" ; "台東縣" ))

在 contact 表中沒有公司名稱，而是指定 Join company On contact::idf = company::id ，透過這個指定，把 company.name 引進來。

### 範例：2

    let (~query ="  
    Select name, name, nameEng, addrCity, addrStr 
    From contact   
    Join company On idf = id   
    Where addrCity = ? 
    Order By addrStr, name " ;
    ExecuteSql ( ~query ; "" ; "" ; "台東縣" ))

這是會發生錯誤的寫法

會出現如:

The column named "name" appears in more than one table in the column reference's scope.

如果兩張表裡有相同的欄位名稱，在敘述中被引用，必須加以完全表示，如範例：1

有關於 debug 請參考第 14 章