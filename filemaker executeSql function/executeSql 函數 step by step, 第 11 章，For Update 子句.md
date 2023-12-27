executeSql 函數 step by step, 第 11 章，For Update 子句
------------------------------------------------

當資料在編輯的狀態下，鎖住取值的動作，而傳會“?”。鎖住的動作在進入記錄中的任何一個欄位被修改時被啟動，如 onModified。

格式為：

    For Update [Of column_expressions]

column\_expressions 是您要更新的數據庫表中的字段名列表，由逗號分隔。

column\_expressions 是可選的，可以忽略。有寫沒寫不會影醒運算的動作，但可以作為提示作用。

### 範例：1

    ExecuteSQL ( "Select name, telAreaCode, telNo From contact For Update" ; "" ; "" )

在表 contact 的任何一筆是在編輯狀態， 便鎖住取值的動作。

### 範例：2

    ExecuteSQL ( "Select name, telAreaCode, telNo From contact Where AddrCity = ? For Update of telAreaCode" ; "" ; "" ; "嘉義市")

在表 contact 的任何一筆 addrCity 是"嘉義市"在編輯狀態， 便鎖住取值的動作。而在編輯 addrCity 不是"嘉義市"的資料，如台北市、新北市⋯⋯等都不會影響取值的動作。

### 範例：3

    ExecuteSQL ( "Select name, telAreaCode, telNo From contact Where name = ? For Update of telAreaCode" ; "" ; "" ; "康斬")

除非康斬的資料是在編輯狀態，其他等都不會影響取值的動作。

### 範例：4

    ExecuteSQL ( "Select name, telAreaCode, telNo From contact Where AddrCity = ? Fetch 10 Rows Only For Update of telAreaCode" ; "" ; "" ; "苗栗縣")

只有前 10 筆被鎖住。

提示：前  10 筆並不是你在 FileMaker 看到的前 10 筆。而是依據 sql 排序的前 10 筆。