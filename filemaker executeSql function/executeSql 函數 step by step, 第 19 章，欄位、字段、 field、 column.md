executeSql 函數 step by step, 第 19 章，欄位、字段、 field、 column
-------------------------------------------------------

*   在 executeSql 這四個名詞指的是相同的，欄位、字段、 field、 column。
*   欄位名稱不區分大小寫。
*   不要使用 sql 保留字。
*   欄位名稱避免使用非英文字元開頭的名字，executeSql 對這種名稱需要特別處理（用雙引號括起來，如 "\_fieldName"、"~fieldName"...）。
*   欄位名稱完整的表示方式：baseTableName.fieldName。
*   •如果只對一個表取值，可以只寫 fieldName。
*   當調用兩個或以上的表時，如果調用的欄位有相同名稱則必須使用完整的表示法。
*   可以使用 alias 讓敘述內容更容易理解，或縮短敘述的長度。
*   影響到 executeSql 效率的欄位類別

1.  summary field：可能有龐大的資料，會影響 excuteSql 效率，剩至於讓 FilMaker 進入無盡的黑洞。
2.  unstored calculation field：運算來自關聯資料表。
3.  unstored calculation field
4.  big data field：內容資料大的欄位。
5.  container field：會轉為檔案名稱。

*   FileMaker 也支援科學符號表示的數字。
*   date, timestamp 欄位 executeSql 取值會自動把日期轉為 yyyy-mm-dd 的格式內容。
*   date, timestamp 欄位不支援 2 位數年度的寫法。