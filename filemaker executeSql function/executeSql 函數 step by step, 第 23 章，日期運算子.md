executeSql 函數 step by step, 第 23 章，日期運算子
----------------------------------------

日期計算的單位：天，日。

在下表中，hire\_date 為 DATE '2028-01-30'

運算子

對日期的影響

示例

結果

+

將天數添加到日期

hire\_date + 5

DATE '2028-02-04'

\-

查找兩個日期之間的天數

hire\_date - DATE '2028-01-01'

29

從日期中減去天數

hire\_date - 10

DATE '2028-01-20'  

範例：1

```
// 取得年齡：
let ([ ~query = "
Select  name, Int ( ( Date'" & get(currentDate) & "' - birthday ) / 365 ) 
From contact 
Where addrCity = '新竹市'
"];
executeSql ( ~query ; char(9) ; "")
)
```