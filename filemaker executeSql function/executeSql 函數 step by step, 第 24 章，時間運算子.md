## executeSql 函數 step by step, 第 24 章，時間運算子

日期計算的單位：秒。

在下表中，time\_now 為 time '18:01:30'

<table style="width: auto; text-align: start;"><tbody><tr><td colspan="1" rowspan="1" width="auto" style="text-align: left;">運算子</td><td colspan="1" rowspan="1" width="auto" style="text-align: left;">對時間的影響</td><td colspan="1" rowspan="1" width="auto" style="text-align: left;">示例</td><td colspan="1" rowspan="1" width="auto" style="text-align: left;">結果</td></tr><tr><td colspan="1" rowspan="1" width="auto" style="text-align: left;">+</td><td colspan="1" rowspan="1" width="auto" style="text-align: left;">將秒數添加到時間</td><td colspan="1" rowspan="1" width="auto" style="text-align: left;">time_now + 100</td><td colspan="1" rowspan="1" width="auto" style="text-align: left;">time '18:12:10'</td></tr><tr><td colspan="1" rowspan="2" width="auto" style="text-align: left;">-</td><td colspan="1" rowspan="1" width="auto" style="text-align: left;">兩個時間之間差異</td><td colspan="1" rowspan="1" width="auto" style="text-align: left;">time_now - time '14:01:01'</td><td colspan="1" rowspan="1" width="auto" style="text-align: left;">time '04:09:29'</td></tr><tr><td colspan="1" rowspan="1" width="auto" style="text-align: left;">從秒數中減去秒數</td><td colspan="1" rowspan="1" width="auto" style="text-align: left;">time_now - 100</td><td colspan="1" rowspan="1" width="auto" style="text-align: left;">time '18:08:50'<br></td></tr></tbody></table>

範例：1

```auto
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

  

