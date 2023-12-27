executeSql 函數 step by step, 第 10 章，Offset 和 Fetch First子句
---------------------------------------------------------

**Offset** 和 **Fetch First** 子句經常搭配使用。限制傳回的資料筆數，取得如“逐頁”瀏覽的效果，並且提高效率。

**Offset 必須寫在** **Fetch First 的前面。**

### **範例：1**

    ExecuteSQL ( "
    Select name, addrStr, addrCity From company Order By addrCity Offset 25 Rows Fetch First 20 Rows Only
    " ; "" ; "" )

略最前面 25 筆，再取省出剩餘的資料的最前面的 20 筆。

### 範例：2

    ExecuteSQL ( "
    Select name, addrStr, addrCity From company Order By addrCity Offset 25 Rows Fetch First 10 Percent Rows Only
    " ; "" ; "" )

略最前面 25 筆，再取省出剩餘的資料的最前面的 10% 的資料筆數。

如果最後一筆可能還有相同 addrCity 沒被傳回，而想要也這個部分也傳回，就需要用 **With Ties**。

    ExecuteSQL ( "
    Select name, addrStr, addrCity From company Order By addrCity Offset 25 Rows Fetch First 10 Percent Rows With Ties
    " ; "" ; "" )