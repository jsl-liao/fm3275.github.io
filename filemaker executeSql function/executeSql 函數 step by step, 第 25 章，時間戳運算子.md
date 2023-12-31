<h2 style="text-align: start;">executeSql 函數 step by step, 第 25 章，時間戳運算子</h2><p style="text-align: start;">日期計算的單位：秒。</p><p style="text-align: start;">在下表中，可以看出 timestamp 可以和 timestamp, date, time 做減法運算</p><table style="width: auto;"><tbody><tr><th colSpan="1" rowSpan="1" width="auto">運算子</th><th colSpan="1" rowSpan="1" width="auto">對時間的影響</th><th colSpan="1" rowSpan="1" width="auto">示例</th><th colSpan="1" rowSpan="1" width="auto">結果</th></tr><tr><td colSpan="1" rowSpan="1" width="auto">+</td><td colSpan="1" rowSpan="1" width="auto">將秒數添加到時間戳</td><td colSpan="1" rowSpan="1" width="auto">timestamp '2023-12-31 18:01:30' + 100</td><td colSpan="1" rowSpan="1" width="auto">'2023-12-31 18:12:10'</td></tr><tr><td colSpan="1" rowSpan="1" width="auto">-</td><td colSpan="1" rowSpan="1" width="auto">兩個時間戳之間差異</td><td colSpan="1" rowSpan="1" width="auto">timestamp '2023-12-31 18:01:30' - timestamp '2023-11-15 14:01:01' </td><td colSpan="1" rowSpan="1" width="auto">'868:09:29'</td></tr><tr><td colSpan="1" rowSpan="1" width="auto">-</td><td colSpan="1" rowSpan="1" width="auto">時間戳減日期</td><td colSpan="1" rowSpan="1" width="auto">timestamp '2023-12-31 18:01:30' - date '2023-11-15'</td><td colSpan="1" rowSpan="1" width="auto">'1122:10:30'</td></tr><tr><td colSpan="1" rowSpan="1" width="auto">-</td><td colSpan="1" rowSpan="1" width="auto">時間戳減時間</td><td colSpan="1" rowSpan="1" width="auto">timestamp '2023-12-31 18:01:30 '- time '14:1:1'</td><td colSpan="1" rowSpan="1" width="auto">'2023-12-31 04:09:29'</td></tr><tr><td colSpan="1" rowSpan="1" width="auto">-</td><td colSpan="1" rowSpan="1" width="auto">時間戳減秒數</td><td colSpan="1" rowSpan="1" width="auto">timestamp '2023-12-31 18:01:30' - 100</td><td colSpan="1" rowSpan="1" width="auto">'2023-12-31 18:08:50'</td></tr></tbody></table><p style="text-align: start;">範例：1</p><pre><code >Let ([
~timestamp_now = Timestamp(Date(12;31;2023);
Time(18;10;30));
~timestamp_alt = Timestamp(Date(11;25;2023); Time(14;1;1));
~date_alt = Date (11;15;2023);
~time_alt = Time (14;1;1);
~no = 100 ;
~query = "
Select 
timestamp'" & ~timestamp_now & "' - timestamp '" & ~timestamp_alt & "',
timestamp'" & ~timestamp_now & "' - date '" & ~date_alt & "',
timestamp'" & ~timestamp_now & "' - time '" & ~time_alt & "',
timestamp'" & ~timestamp_now & "' + " & ~no  & ",
timestamp'" & ~timestamp_now & "' - " & ~no  & " From dev 
"];
ExecuteSQL ( ~query ; ¶ ; ""))</code></pre><p><br></p>