executeSql 函數 step by step, 第 24 章，時間運算子
----------------------------------------

日期計算的單位：秒。

在下表中，time\_now 為 time '18:01:30'

運算子

對時間的影響

示例

結果

+

將秒數添加到時間

time\_now + 100

time '18:12:10'

\-

兩個時間之間差異

time\_now - time '14:01:01'

time '04:09:29'

從秒數中減去秒數

time\_now - 100

time '18:08:50'  

範例：1

```
// 第一個值: 兩個時間相減
// 第二個值: 時間加 100 秒
// 第三個值: 時間減 100 秒
let ([
~time_now = time (18;10;30);
~time_alt = time (14;01;01);
~no = 100 ;
~query = "
Select time'" & ~time_now & "' - time '" & ~time_alt & "',
time'" & ~time_now & "' + " & ~no  & ",
time'" & ~time_now & "' - " & ~no  & "
From dev 
"];
executeSql ( ~query ; ¶ ; ""))
```