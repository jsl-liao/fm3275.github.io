executeSql 函數 step by step, 第 8 章，Offset 子句
-------------------------------------------

Offset 子句指示在開始返回數據之前要跳過的行數。如果 OFFSET 子句未在 SELECT 語句中使用，則起始行為 0。

子查詢不支援 Offset。

格式為：

    Offset [ n {Rows | Row} ]

`n` 是無符號整數。

如果 `n` 大於結果集中返回的行數，則不返回任何內容，並且不顯示錯誤消息。

ROWS 與 ROW 相同。

範例：1

    ExecuteSQL ( "
    Select addrStr, addrCity, name From contact Where addrCity = ? Order By nameEng Offset 25 Rows
    " ; "" ; "" ; "新北市" )

獲得的前 25 筆資料被省略。