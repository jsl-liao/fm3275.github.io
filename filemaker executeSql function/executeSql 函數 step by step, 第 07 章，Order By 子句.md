executeSql 函數 step by step, 第 7 章，Order By 子句
---------------------------------------------

`ORDER BY` 子句指示如何排序記錄。如果 `SELECT` 語句不包含 `ORDER BY` 子句，記錄可能會按任意順序返回。

格式為：

    Order By {sort_expression [DESC | ASC]}, ...

sort\_expression 可以是字段名或要使用的列表達式的位置編號。默認為執行升冪 (ASC) 排序。

FileMaker Server 使用 Unicode 二進制排序順序，它不同於 FileMaker Pro 中或使用默認中性語言排序順序的語言排序。區分大小寫。

範例：1

    ExecuteSQL ( "Select name, nameEng, addrCity, addrStr From contact Where addrCity = ? Order By nameEng ";", " ; "" ; "花蓮縣" )

依據英文名字排序，區分大小寫。

    ExecuteSQL ( "Select name, nameEng, addrCity, addrStr From contact Where addrCity = ? Order By Lower (nameEng) ";", " ; "" ; "花蓮縣" )

使用 Lower 或 Upper 函數，進行不區分大小寫的排序。