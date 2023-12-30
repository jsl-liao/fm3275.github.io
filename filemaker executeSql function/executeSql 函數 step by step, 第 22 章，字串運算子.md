executeSql 函數 step by step, 第 22 章，字串運算子
----------------------------------------

可以用 “+“ 或 ”-“ 把字串連接起來。

您可以將多個字元連接起來。在下表中，`last_name` 為 `'JONES '`，first\_name 為 `'ROBERT '`。

運算子

串聯

示例

結果

+

保留末尾的空格字元

first\_name + last\_name

'ROBERT JONES '

\-

將末尾的空格字元移到最後

first\_name - last\_name

'ROBERTJONES '

||

串連運算子

first\_name || last\_name

'ROBER TJONES '

### 範例：1

```
executeSql("Select '尾巴3個空白   ' + '  最前面2個空白.結果: 5個空白在兩個字串之間, 尾巴無空白' from dev"; "" ;"")
// 尾巴3個空白     最前面2個空白.結果: 5個空白在兩個字串之間, 尾巴無空白
```

### 範例：2

```
executeSql("Select '尾巴3個空白   ' - '  最前面2個空白.結果: 2個空白在兩個字串之間, 尾巴3個空白' from dev"; "" ;"")
// 尾巴3個空白  最前面2個空白.結果: 2個空白在兩個字串之間, 尾巴3個空白   
```

### 範例： 3

```
executeSql("Select '前面的字串 ,' || '後面的字串.結果: 兩個字串直接連接在一起' from dev"; "" ;"")
// 前面的字串 ,後面的字串.結果: 兩個字串直接連接在一起
```

  

