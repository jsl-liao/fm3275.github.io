executeSql 函數 step by step, 第 4 章，Group 子句
------------------------------------------

GROUP BY 子句指定返回的值應按其分組的一個或多個字段的名稱。此子句用於返回一組聚合值。它具有以下格式：

    GROUP BY 列 // column

GROUP BY 子句的範圍是 FROM 子句的表達式。

因此，columns 指定的列表達式必須來自 FROM 子句中指定的表。

列表達式可以是以逗號分隔的數據庫表的一個或多個字段的名稱。

Group 子句和聚合函數一起應用。

Group 要放在正確的位置，如第 0 章所敘述的順序。

範例 1:

從 company 取得每個縣市的公司數, 並組成 json

    While (  
      [    
        ~cityList = ExecuteSQL ( "Select Distinct (addrCity) From company" ; "" ; "");    
        ~end = ValueCount ( ~cityList );    
        ~i = 1 ;    
        ~json = "{}" ;    
        ~endInitial = True  
      ];  
      ~i <= ~end ;  
      [    
        ~city = GetValue (~cityList ; ~i );    
        ~ids = ExecuteSQL ( "Select id From company Where addrCity = ?" ; "" ; "" ; ~city );    
        ~qty = ValueCount(~ids);    ~json = JSONSetElement ( ~json ; ~city ; ~qty ; 2 );    
        ~i = ~i + 1  
      ];  
      substitute ( JSONFormatElements ( ~json ) ; char(9) ; "  "))

用 Group 子句達成相同的結果

    let (  
      ~json = "{\"" & ExecuteSQL ( "Select addrCity , count(id) From Company Group By addrCity" ; "\":" ; ",\"" ) & "}";  
      substitute ( JSONFormatElements ( ~json ) ; char(9) ; "  "))

提示:

1.  json 是字串資料, 用 column separator 和 row separator 和處理字串的手法, 可以組成 json 資料
2.  JSONFormatElements 除了提供更好檢視的內容，他還可以加速 data viewer 中 render 資料的速度，尤其在大資料的  json 更明顯。