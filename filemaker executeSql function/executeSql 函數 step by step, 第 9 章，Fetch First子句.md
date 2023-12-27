executeSql 函數 step by step, 第 9 章，Fetch First子句
-----------------------------------------------

**Fetch First** 子句以大於或等於 1 的無符號整數或者百分比的形式指示從 OFFSET 子句中指示的起點開始要返回的行數。

格式為：

    Fetch First [ n [ Percent ] ] { Rows | Row } {Only | Wtith Ties } ]

**n** 是要返回的行數。如果省略 n，則默認值為 1。

**n** 是大於或等於 1 的無符號整數，除非其後面是 PERCENT。如果 n 後面是 PERCENT，則值是正小數值或者是無符號整數。

**Rows** 與 **Row** 相同。

**With Ties**

傳回 **Fetch First** 結果的最後一個位數繫結的資料列。 您必須搭配 **Order By** 子句使用這個引數。 **With Ties** 可能會導致傳回比 n 值更多的資料列。

### 範例：1

    ExecuteSQL ( "Select name, addrStr, addrCity From company Order By addrCity Fetch First 20 Rows Only" ; "" ; "" )

沒有使用 **With Ties** 傳回剛剛好前 20 筆資料, 包括**南投縣的全部公司**和**台中市的****部分****公司**。

### 範例：2

    ExecuteSQL ( "
    Select name, addrStr, addrCity From company Order By addrCity Fetch First 10 Percent Rows Only
    " ; "" ; "" )

沒有使用 **With Ties** 傳回剛剛好前 10% 的筆數資料, 包括**南投縣的全部公司**和**台中市的部分公司**。

### 範例：3

    ExecuteSQL ( "
    Select name, addrStr, addrCity From company Order By addrCity Fetch First 20 Rows With Ties
    " ; "" ; "" )

使用 **With Ties** 傳回可能超過 20 筆的資料, 包括**南投縣的全部公司**和**台中市的全部公司**。