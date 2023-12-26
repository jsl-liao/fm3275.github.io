executeSql 函數 step by step, 第 3 章，Select...From， 最基本的查詢
=======================================================

SELECT ...FROM 子句指示在 SELECT 語句中使用的表。格式為：

    executeSql ( "SELECT column_expression [AS] column_alias FROM table_name [table_alias] [, table_name [table_alias]]" ; column_separator ; row_separator {;arguments}) 

### column\_expression

就是 FileMaker  的 field 欄位名稱，不含表名稱。您要檢索的列表達式（例如 last\_name）。表達式可以包括數學運算或字串操作（例如，SALARY \* 1.05）。

### column\_alias

可用於為列提供更具描述性的名稱，或縮寫較長的列名稱。字段名可以以表名稱或表别名為前綴。例如，EMP.LAST\_NAME 或 E.LAST\_NAME，其中 E 是表 EMP 的别名。

### table\_name

`table_name` 是數據庫中表的名稱。表名稱必須以字母字元開頭。如果表名稱以非字母字元開頭或包含點 (.)，則用雙引號將其括起來（帶引號的標識符）。

### `table_alias`

可用於為表提供更具描述性的名稱，以縮寫較長的表名稱，或在查詢中（例如，在自身連接中）多次包括同一個表。

字段名以字母字元開頭。如果字段名以非字母字元開頭或包含點 (.)，則用雙引號將其括起來（帶引號的標識符）。

### column\_separator

查詢取得的資料的列（欄位, field）資料的分隔符號, 可以是單一字元，字串。

最後一個 column 後面不會有尾隨的 column\_separator。

如果是寫成""，表示用預設的分隔符號 ","。

如果欄位的資料中有分隔符號，會被視為分隔符號，產生錯誤的資料分隔，則必須使用不同的分隔符號避免錯誤的發生。

### row\_separator

查詢取得的資料的行（記錄, reocrd）資料的分隔符號, 可以是單一字元，字串。

最後一個 row 後面不會有尾隨的 row\_separator。

如果是寫成""，表示用預設的分隔符號 "¶" （return , char(13)）。

如果記錄的資料中有分隔符號，會被視為分隔符號，產生錯誤的資料分隔，則必須使用不同的分隔符號避免錯誤的發生。

### argument

引數是和敘述中的“？”對應的，在把敘述轉譯為執行碼時會依據順序以引數取代“？”。

這個寫法常用於表示 Where 子句中用來的比對的值。

* * *

### 範例 1

    ExecuteSQL ( "Select * From contact" ; "" ; "" )

從 table: contact 取出所有的紀錄的所有的欄位, 包括 summary field

容器欄位則會取得檔案名稱

### 範例 2

    ExecuteSQL ( "Select name, nameEng, \"_addrZip\", addrCity From contact" ; "" ; "" )

欄位名稱以預設的欄位分隔符號"," 作為欄位分隔符號。記錄以預設的記錄分隔符號"¶" 作為記錄分隔符號。

如果欄位名稱，表名稱以非字母字元開頭或包含點 (.)，則用雙引號將其括起來（帶引號的標識符）。

### 範例 3

    ExecuteSQL ( "Select name, nameEng, \"_addrZip\", addrCity From contact Where addrCity = ?" ; "" ; "" ; "新北市")

使用引數來表示 Where 子句中比對的值, 以“?“表示。

其效果和下面的寫法是相同的。

    ExecuteSQL ( "Select name, nameEng, \"_addrZip\", addrCity From contact Where addrCity = '新北市'" ; "" ; "" )

### 範例 4

    ExecuteSQL ( "Select name, nameEng, stroke, addrCity From contact Where addrCity = ? Order By stroke"; "" ; "" ; "新北市" )

引數不適用於 Order By 子句。