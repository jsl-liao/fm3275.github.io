executeSql 函數 step by step, 第 20 章，常數
-------------------------------------

*   字串常數：用單引號括起來，如 '這是一個常數'。

 要在用單引號括起的字元常數中加入單引號，請同時使用兩個單引號（例如，'Don''t'）。

*   日期常數： Date '2023-12-31'，"Select date '" &  get(currentDate) & " ' From oneRecord"。

 不支援 2 位數年的語法。

*   時間常數：Time '14:14:14', "Select time '" & get(currentTime) & " ' From oneRecord"。
*   時間戳常數：Timestamp '2023-12-31 14:14:14', "Select timestamp '" & get(currentTime) & " ' From oneRecord"。

 不支援 2 位數年的語法。

範例：1

```
let ([
~query = "
Select  name, Int ( ( Date'" & get(currentDate) & "' - birthday ) / 365 ), '歲' 
From contact 
Where addrCity = '新竹市'
"];
executeSql ( ~query ; char(9) ; ""))
```

計算出年齡

下面這個寫法漏掉單引號，會發生：An expression contains incompatible data types.

```
let ([
~query = "
Select  name, Int ( ( Date" & get(currentDate) & " - birthday ) / 365 ), '歲' 
From contact 
Where addrCity = '新竹市'
"];
executeSql ( ~query ; char(9) ; ""))
```