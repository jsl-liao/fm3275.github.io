executeSql 函數 step by step, 第 18 章，column separator 和 row column separator
--------------------------------------------------------------------------

column separator，也可以稱為 field separator

row separator, 也可以稱為 record separator

separator 的作用

*   產生特定格式資料。
*   透過設定可以產生如：string, json, html, csv(內定 separator 產生的格式 common separate value)...
*   如果取值的資料中有“,“ 或 ¶，可以用 separator 加以處理，避免錯誤的資料處理，導致錯誤的結果。

### 範例：1

    let (  ~json = "{\"" & ExecuteSQL ( "Select addrCity , count(id) From Company Group By addrCity" ; "\":" ; ",\"" ) & "}";  
    substitute ( JSONFormatElements ( ~json ) ; char(9) ; "  "))

產生 json data

### 範例: 2

    ExecuteSQL ( "Select name, addrStr, addrCity From company" ; char(41444) ; char(41445) )

如果取值的資料中有“,“ 或 ¶，可以用 separator 加以處理。

後續的資料處理可以用 custom function：cf\_strByDiv處理，cf\_strByDiv 在 custom function 的資料夾內。

### 範例：3

    let ([  
    ~format = "tsv" ;  
    ~colSep = case ( ~format = "json" ;  "\":" ; ~format = "html" ; "" ;~format = "tsv"; char(9) ; "" );  
    ~rowSep = case ( ~format = "json" ;  ",\"" ; ~format = "html" ; "¶" ; ~format = "tsv"; char(10) ; "" );  
    ~prefix = case ( ~format = "json" ;  "{\"" ; ~format = "html" ; "" ; ~format = "tsv"; "" ; "" );  
    ~tail = case ( ~format = "json" ;  "}" ; ~format = "html" ; "" ; ~format = "tsv"; "" ; "" );  
    ~query = "Select addrCity , count(id) From Company Group By addrCity" ];  
    ~prefix & ExecuteSQL ( ~query ; ~colSep ; ~rowSep ) & ~tail)

各縣市公司數的統計表，改變 ~format 則傳回不同格式的值。

~format 可以是 json, html, tsv 其他則是用內定的 csv 格式。