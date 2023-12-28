executeSql 函數 step by step, 第 13 章，Select 敘述的安全寫法
-------------------------------------------------

### 作法

1.  在 data viewer 輸入 Select 敘述，欄位名稱使用完全限定名稱（ fully qualified name , tableName::fieldName ）
2.  把 “::" 置換成 “.“，轉換成 executeSql 合法敘述。
3.  應用於 Join 子句的狀況下，不同表的取值的欄位如果有相同名稱必須加表的標示，否則會發生錯誤。
4.  這個方法好用之處在於：在 data viewer 左邊的欄位區域雙擊欄位變可以取得完全限定名稱，避免手動輸入的錯誤。
5.  如果 executeSql 只對一個表取值，也可以應用。

### 範例：

    let (
    [
    ~queryFake ="  
    Select company::name, contact::name, contact::nameEng, contact::addrCity, contact::addrStr 
    From contact   
    Join company On contact::idf = company::id   
    Where contact::addrCity = ? 
    Order By contact::addrStr, contact::name " ;
    ~query = substitute ( ~queryFake ; "::" ; "." )
    ];
    ExecuteSql ( ~query ; "" ; "" ; "台東縣" ))