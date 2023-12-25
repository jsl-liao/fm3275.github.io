**FileMaker 的 executeSql 函數 step by step, 第 0 章**

**SELECT 敘述可以包含多個子句**

    SELECT [ DISTINCT ] { * | column_expression [[AS] column_alias],...} 
    FROM table_name [ table_alias ], …
    [ JOIN clause]
    [ WHERE expr1 rel_operator expr2 ]
    [ GROUP BY { column_expression, ...} ]
    [ HAVING expr1 rel_operator expr2 ]
    [ UNION [ ALL ] ( SELECT...) ]
    [ ORDER BY { sort_expression [ DESC | ASC ] }, ... ]
    [ OFFSET n { ROWS | ROW} ]
    [ FETCH FIRST [ n [ PERCENT ] ] { ROWS | ROW } { ONLY | WITH TIES } ]
    [ FOR UPDATE [ OF {column_expression, ...}] ]

sql 查詢語句必要的兩部分構成，第一部分是要 "拿什麼" 資料 (若有多項用逗號隔開)；第二部分則為 "從哪拿"。

    SELECT table_column1, table_column2, table_column3...
    FROM table_name;

**sqlQuery: sql 查詢語句, 只支援 select 查詢**

*   避免表名稱和欄位名稱和 sql 保留字衝突, 衝突發生雖可處理, 但應避免。
*   欄位別名(使用 As 指定)用來語義化欄位或者用較短名稱來標示欄位。
*   executeSql 查詢是獨立於上下文(context), 可以查詢非目前表或關聯表的資料。
*   返回的數據是純文字, 可以透過文字相關函數進行處理。
*   語句中的 sql 關鍵字，欄位名稱，表名稱都不區分大小寫。
*   值是區分大小寫的。
*   查詢語句可以用多個子句組合。
*   如果是多個子句構成的 sql 查詢，遵照上面列出的子句順序書寫是最安全的寫法。錯誤的順序可能導致語法錯誤或者邏輯性的錯誤。
*   white space 為分隔符號, 連續的  white space 效果如一個 white space。
*   table name 必須是在 table 的 relation graph 中有出現的 base table name。
*   field name 必須是純欄位名稱(不包含 table name)或者 tableName.fieldName。
*   任何錯誤的 field name, table name 或語法錯誤, 會返回 "?"。
*   可以一次查詢多個欄位, 欄位間以 "," 隔開。
*   字串常數如果放在語句中, 用單引號括起來。
*   可以查詢引入的外部資料庫的表。
*   要獲得數據可能有好幾種計算式寫法, 從幾種計算式測試哪一個表較合適。
*   雖然 executeSql 可以在語句內使用備註, 建議備註使用在語句外。
*   通常越複雜的計算式表示計算越耗時, 精簡的計算式, 通常是有利的寫法。
*   取得的數據越大表示越長的計算時間, 選擇只取得的必要數據, 是有利的寫法。
*   在寫 executeSql 計算式要注意: 拼字, 標點符號, 語句的順序。
*   executeSql 不接受 emoji 的資料輸入。
*   executeSql 的運算結果是文字類型資料, 即使是用 count, sum 取得的值, 不區分大小寫如果要與數字, 日期, 時間做比較, 都必須 getAsNumber, GetAsDate, ... 處理, 否則會發生邏輯性錯誤。

fieldSeparator: 欄位分隔符號或稱為 column separator

*   可以是任何文字。
*   如果輸入"" 則使用內定值 ","。

**rowSeparator: 記錄分隔符號, 區隔獲取的資料的不同紀錄**

*   可以是任何文字。
*   如果輸入"" 則使用內定值 "¶" 即 return, char(13)。

**arguments: 引數**

*   用於 where 子句的鍵值。
*   argument 的內含區分大小寫。
*   如果有多個條件, argument 用 "," 分開。
*   sqlQuery 的 where 子句中的 "?” 依序對應於 arguments。
*   where 子句依序取用 arguments, 多餘的 argument 被忽略。

**executeSql 的應用**

*   獨立於上下文關係的運算, 非關係資料表的取值。
*   減少關聯資料表。
*   減少欄位數。
*   產生格式化的計算結果。
*   配合 script 可以輸出成客製化的文字檔案。
*   配合在 one record table 的欄位, 可以達成在 script 就完成 value List。
*   取得外部檔案的資料表(未引入的資料表)的資料( 需要安裝必要的 Plugin )。

executeSql 的應用時機  
executeSql 的計算不是即時的, 是需要被觸發的

*   不要應用到定義計算欄位的計算式, 除非 Store Options 設定為 "Do not store calculated results - -recalculate when needed"。
*   不要應用到欄位定義的 Auto Enter 的 calculated Value, 定義, 除非 設定為 "Do not replace existing value of field ( if any)”。
*   不要應用到佈局的 conditional formatting 和 hide object when。
*   在 script  中的計算式。
*   或者 script trigger 中的計算式。
*   產生常數儲存到 global field 或 global variable。

**executeSql 的技巧**

*   如果計算式太長, 可按照語句分開。
*   利用 let 函數, 產生模組化, 彈性的計算式內容。
*   備註( 寫在 executeSql 計算式外面, 雖然語句內也可以寫備註) 。
*   使用程式碼編輯器, 如 visual studio code, TextMate, BBEdit, Sublime Text,…。
*   修改計算式前, 先備份。
*   利用 substitute ( getFieldName( field ) ; “::” ; “.” ) 轉成 tableName.fieldName 。
*   如果是經常使用的 Select 敘述，可以寫成 custom function。