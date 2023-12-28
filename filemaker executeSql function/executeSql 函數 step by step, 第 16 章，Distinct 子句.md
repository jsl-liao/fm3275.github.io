executeSql 函數 step by step, 第 16 章，Distinct 子句
----------------------------------------------

*   **Distinct** 運算子只能放在第一個列表達式（column, field, 欄位）之前。
*   **Distinct** 消除了查詢結果中的重複行。
*   一個 **Select** 敘述只能有一個 **Distinct**。
*   **Distinct** 區分大小寫，如果要不分大小寫，可用 Lower 或 Upper 函數。
*   **Distinct** 的欄位有沒有用小括號括起來都是合法的寫法。

### 範例：1

    ExecuteSQL ( "Select Distinct (addrCity) From company" ; "" ; "")

列出縣市，傳回值是一個 value list。

### 縣市：2

    ExecuteSQL ( "Select Distinct nameEng, name, addrStr From contact Where AddrCity = ?" ; "" ; "" ; "嘉義市")

在 nameEng, name, addrStr 都不相同時，才會被 sql 視為 Distinct，這是錯誤使用 Distinct 的範例。

### 範例：3

    ExecuteSQL ( "Select Distinct Lower(nameEng) From contact Where addrCity = ?" ; "" ; "" ; "金門縣")

用 Lower 函數進行不分大小寫的 **Distinc**t。