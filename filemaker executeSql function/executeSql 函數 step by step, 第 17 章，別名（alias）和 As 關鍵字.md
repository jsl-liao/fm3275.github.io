executeSql 函數 step by step, 第 17 章，別名（alias）和 As 關鍵字
----------------------------------------------------

### alias 的作用

*   讓敘述更語易化，更容易理解敘述的含義。
*   欄位名稱和表名稱都可以使用 alias 。
*   As 關鍵字可以省略不寫。
*   在複雜的敘述中，縮短敘述長度，精簡內容。

### 範例：1

    let (  [    
    ~query = "
    Select name, nameEng, addrCity, addrStr 
    From contact Where addrCity = ?
    "];  
    ExecuteSql ( ~query ; "" ; "" ; "連江縣" ))

    let (  [    
    ~query = "
    Select name chinese_name, nameEng english_name, addrCity city, addrStr street 
    From contact Where addrCity = ?
    "];  
    ExecuteSql ( ~query ; "" ; "" ; "連江縣" ))

    let ([
    ~query = "
    Select name As chinese_name, nameEng As english_name, addrCity As city, addrStr As street 
    From contact Where addrCity = ?
    "];
      
    ExecuteSql ( ~query ; "" ; "" ; "連江縣" )
    )

上面這三個寫法的作用完全相同。第二、三種寫法讓敘述內容更語意化。

有得有寫 As 有得沒寫 As 並不會影響結果。

範例：2

    Let (
    [
    ~query =
    "
      
    Select y.name, c.name, c.nameEng, c.addrCity, c.addrStr 
      
    From contact C  
      
    Join company Y On C.idf = Y.id    
      
    Where C.addrCity = ? 
      
    Order By C.addrStr, C.name 
    " 
    ];
    
    ExecuteSQL ( ~query ; "" ; "" ; "台東縣" )
    )

    let ([~query ="  
    Select company.name, contact.name, contact.nameEng, contact.addrCity, contact.addrStr   
    From contact    
    Join company On contact.idf = company.id      
    Where contact.addrCity = ?   
    Order By contact.addrStr, contact.name 
    " ];
    ExecuteSql ( ~query ; "" ; "" ; "台東縣" ))

上面這兩個寫法的作用完全相同。第ㄧ種寫法讓敘述內容更精簡。

在複雜的敘述中，選擇用完整的寫法或者完全的精簡寫法，不要混用，否則會出錯。