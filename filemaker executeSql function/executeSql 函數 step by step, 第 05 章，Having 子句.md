executeSql 函數 step by step, 第 5 章，Having 子句
-------------------------------------------

利用 HAVING 子句可以為記錄組（  Group ）指定條件，一定是和 Group 子句搭配 一起使用。

    GROUP clause HAVING expr1 rel_operator expr2

`expr1` 和 `expr2` 可以是字段名稱、常量值或表達式。這些表達式不必匹配 `SELECT` 子句中的列表達式。

`rel_operator` 是連結兩個表達式的關係運算子。

### 範例 1:

列出公司家數大於 12 家的縣市, 和公司家數, 組成  json

和第 4 章的範例比較, 只差了 Having 子句
```dotnetcli
let (
  ~json = "{\"" & ExecuteSQL ( "Select addrCity , count(id) From Company Group By addrCity Having Count(id) > 12" ; "\":" ; ",\"" ) & "}";
  substitute ( JSONFormatElements ( ~json ) ; char(9) ; "  "))
```
    

### 提示:

1.  為了更容易閱讀和除錯, 可以把計算式依據子句做分段。
2.  子句的順序要如第０章所列出的順序。
```
let (  
  ~json = "{\"" & ExecuteSQL ( "    
    Select addrCity , count(id)     
    From Company     
    Group By addrCity     
    Having Count(id) > 12     
    " ; "\":" ; ",\"" ) & "}";  
  substitute ( JSONFormatElements ( ~json ) ; char(9) ; "  "))
```