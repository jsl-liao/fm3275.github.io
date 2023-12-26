executeSql 函數 step by step, 第 3 章，Where 子句與比較運算子
------------------------------------------------

WHERE 子句指定要檢索的記錄必須符合的條件。WHERE 子句包括以下形式的條件：

    WHERE expr1 rel_operator expr2

`expr1` 和 `expr2` 可以是字段名稱、常數或表達式。

`rel_operator` 是連結兩個表達式的關係運算子。


| 比較運算子 | 說明 | 補充 |
|---|---|---|
|=|等於||
|<> 或 !=|不等於|不可以用 FileMaker 的運算符號： ≠|
|>|大於||
|>= 或 !<|大於或等於|不可以用 FileMaker 的運算符號： ≥|
|<|小於||
|<= 或 !>|小於或等於|不可以用 FileMaker 的運算符號： ≤|

executeSql 的比較運算子只能用於 Where 子句。

必須是相同的 type 的資料之間才能做運算。

只使用 = 比使用 >, <, >=, <= 的運算速度快。

### 範例 1:

找出英文名字是以 "T"或 “T”以後的字母開頭的姓名和英文名字
```filemaker function: 
ExecuteSQL ( "Select name, nameEng From contact Where nameEng >= 'T'" ; "" ; "")
```
比較的值是區分大小寫的，如果'T'寫成't'，可能會找不到資料，因為習慣上名字的第一個字母會用大寫。ASCII 小寫字母排在大寫字母後面。
```filemaker function: 
ExecuteSQL ( "Select name, nameEng From contact Where nameEng >= 't'" ; "" ; "")
```
### 範例 2:

找出住址在花蓮縣“且”是女性的人的名字和 email
```filemaker function: 
ExecuteSQL ( "Select name, email From contact Where addrCity ='花蓮縣' and  gender='女'" ; "" ; "")
```
Where 可以用 And （且），Or（或）進行多重條件的資料過濾。

### 範例 3:

找出住址在花蓮縣“且”是女性 或者是住址在台東縣“且”是女性的人的名字和 email
```filemaker function: 
ExecuteSQL ( "Select name, email From contact Where  ( addrCity ='花蓮縣' and  gender='女' ) OR ( addrCity ='台東縣' and  gender='女' )" ; "" ; "")
```
多重的過濾條件可以用（）來加以組合