FileMaker 的 executeSql 函數 step by step, 第 1 章，executeSql 錯誤訊息列表
---------------------------------------------------------------

### executeSql 錯誤訊息列表

*   There is an error in the syntax of the query.

可能是以下狀況

Group By 子句不可以和 Fetch First 或 Offset 子句一起使用

executeSql  的參數,常數, 值不接受  emoji, sfPro 字型的輸入; 否則會發生

*   The table named "0" does not exist.

指定的表名稱為 “0” 的表不存在。

*   The table named "0" already exists in this query.

指定的表名稱為 “0” 的表重複出現。

*   The query is too complex. The maximum number of tables has been exceeded.

查詢太複雜。 已超出最大的表允許數。

*   Expressions involving aggregations are not supported.

查詢的敘述不支援涉及聚合的表達式。

*   The column named "0" appears in more than one table in the column reference's scope.

名為 “0” 的列（欄位, field )）出現在列引用範圍內的多個表中。

在多個表中都有相同欄位名稱時，可能發生的狀況，可以用 alias（關鍵字 AS ）避免發生這種錯誤。

*   The column named "0" does not exist in any table in the column reference's scope.

名為“0”的欄位不存在於列引用範圍內的任何表中。

*   The table named "0" does not exist in the column reference's scope.

在 Select 子句中的 column name 所在的 table 未出現在 From 子句的 row name 中。

表示: 這個 TableName 應該用 Join 子句或者 Where 子句產生關係, 才可以運算。

*   The column named "1" does not exist in table "0".

表“0”中不存在名為“1”的欄位。

*   The literal value "0" is not a valid DATE, TIME or TIMESTAMP.

文字值“0”不是有效的日期、時間或時間戳。

*   Predicate must contain a logical operation (=, <, OR, AND, IS NULL, ...).

必須包含邏輯運算（=、<、OR、AND、IS NULL、...）。

*   The ordinal reference "0" in the ORDER BY clause is not valid.

ORDER BY 子句中的序號引用“0”是無效的。

*   Incompatible types in assignment.

賦值中的型別不相容。

*   The number of values in a VALUES row value constructor does not match the number of values in the target.

VALUES 行值建構函數中的值數量與目標中的值數量不符。

*   The number of values in an INSERT...SELECT statement does not match the number of values in the target.

INSERT...SELECT 語句中的值數量與目標中的值數量不符。

*   A subquery contains an illegal outer reference to a column in the INSERT's target table.

子查詢包含對 INSERT 目標表中列的非法外部參考。

*   An expression contains data types that cannot be compared.

表達式包含無法比較的資料類型。

*   An expression contains incompatible data types.

可能是:以下的狀況

Coaleesce 內的 column 的 data type 不同

用  || 串接數字與數字

*   The result data type of a CASE expression cannot be inferred; they are all NULL.

無法推斷 CASE 表達式的結果資料型態； 它們都是 NULL。

*   An invalid number of parameters was supplied to the function "0".

向函數“0”提供的參數數量無效。

*   Parameter number 0 to the function "1" is not of the correct type.

argument  必須符合函數的類型, 例如字串函數要對日期值取值需要用 strVal ( date value )

*   A subquery expression must have exactly one value in the SELECT list.

子查詢運算式在 SELECT 清單中必須只有一個值。

*   A CAST expression requested an invalid data type conversion

CAST 表達式請求無效的資料型別轉換。

*   A reference to ROWID must be qualified if more than one table is present in the query.

如果查詢中存在多個表，則必須限定 ROWID 的參考。

*   All non-aggregated column references in the SELECT list and HAVING clause must be in the GROUP BY clause.

當 Select 子句同時有不在 aggregate function 的欄位和在 aggregate function 的欄位, 不在 aggregate function 的欄位都必須在 Group By 子句出現

*   The number of columns in both inputs to a UNION operation must be the same.

UNION 運算的兩個輸入中的列數必須相同。

*   The data types of corresponding columns in the inputs to a UNION operation must be the same.

UNION 運算的輸入中對應列的資料類型必須相同。

*   Field repetitions must be numeric and between 1 and 0.

欄位重複必須是數字且介於 1 和 0 之間。

*   A field repetition in the SET clause of an UPDATE statement must be a constant.

UPDATE 語句的 SET 子句中的欄位重複必須是常數。

*   "0" is an invalid function.

所列出的函數不是合法的函數

*   The the parameter's type cannot be inferred in this context. At least one query parameter must be an expression, a column or a constant.

在此上下文中無法推斷參數的類型。 至少一個查詢參數必須是表達式、列或常數。

*   A query may contain either named parameters or dynamic parameters, but not both.

查詢可以包含命名參數或動態參數，但不能同時包含兩者。

*   Column names in FROM clause subqueries must be unique.

查詢可以包含命名參數或動態參數，但不能同時包含兩者。

*   The number of output columns in a FROM clause subquery must match the number of columns in the table's name list.

FROM 子句子查詢中的輸出列數必須與表格名稱清單中的列數相符。

*   Cursor support is not enabled for this query.

此查詢未啟用遊標支援。

*   A cursor with the name "0" already exists.

名稱為「0」的遊標已存在。

*   There is no cursor with the name "0".

沒有名稱為“0”的遊標。

*   The cursor "0" is already open.

遊標“0”已經開啟。

*   The cursor "0" is not open.

遊標“0”未開啟。

*   The target cursor "0" does not reference a query that is valid for WHERE CURRENT OF .

目標遊標「0」未引用對 WHERE CURRENT OF 有效的查詢。

*   The target cursor "0" does not reference the same table as the current statement.

目標遊標「0」未引用與目前語句相同的表。

*   The default value for column "0" does not match the column's data type.

列“0”的預設值與該列的資料類型不符。

*   The string "0" is not a valid stream name.

字串“0”不是有效的流名稱。

*   The column "0" is not valid in this context. The targets of GETAS and PUTAS must be Container fields.

列“0”在此上下文中無效。 GETAS 和 PUTAS 的目標必須是 Container 欄位。

*   The value 0 is not a valid binary string.

值 0 不是有效的二進位字串。

*   Container fields are not allowed in UNION DISTINCT queries.

UNION DISTINCT 查詢中不允許使用容器欄位。

*   The database schema has changed. This prepared query is no longer valid.

資料庫架構已更改。 這個準備好的查詢不再有效。

*   This statement contains an invalid operation on FileMaker system table "0".

該語句包含對 FileMaker 系統表「0」的無效操作。

*   Aggregation expressions are not allowed in the WHERE clause.

Where 子句中不可以有聚合函數

*   The offset count in OFFSET clause is not valid..

OFFSET 子句中的偏移量計數無效。

*   The FETCH ... WITH TIES clause is not allowed without a corresponding ORDER BY clause.

如果沒有對應的 ORDER BY 子句，則不允許使用 FETCH ...WITH TIES 子句。

*   The fetch count in FETCH clause is not valid.

FETCH 子句中的提取計數無效。

*   An invalid number of parameters was supplied to the function “COALESCE"

COALESCE ( expressions ), expression 最少要有兩個