<h2>executeSql 函數 step by step, 第 20 章，常數</h2><ul><li>數字常數：支援科學記號，例如：3.4e7 或 3.4E7。</li><li><span style="color: rgb(0, 0, 0);">字串常數：用單引號括起來，例如 '這是一個常數'。</span></li></ul><p><span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;"> &nbsp;要在用單引號括起的字元常數中加入單引號，請同時使用兩個單引號（例如，</span>'Don''t'<span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;">）。</span></p><ul><li>日期常數： Date '2023-12-31'，"Select date '" & &nbsp;get(currentDate) & " ' From oneRecord"。</li></ul><p> &nbsp;不支援 2 位數年的語法。</p><ul><li>時間常數：Time '14:14:14', <span style="color: rgb(0, 0, 0);">"Select time '" &amp; get(currentTime) &amp; " ' From oneRecord"。</span></li><li><span style="color: rgb(0, 0, 0);">時間戳常數：Timestamp '2023-12-31 14:14:14', "Select timestamp '" &amp; get(currentTime) &amp; " ' From oneRecord"。</span> </li></ul><p><span style="color: rgb(0, 0, 0);"> &nbsp;不支援 2 位數年的語法。</span></p><h3>範例：1</h3><p><span style="color: rgb(0, 0, 0);">計算出年齡</span></p><pre><code >let ([
~query = "
Select  name, Int ( ( Date'" & get(currentDate) & "' - birthday ) / 365 ), '歲' 
From contact 
Where addrCity = '新竹市'
"];
executeSql ( ~query ; char(9) ; ""))</code></pre><p>下面這個寫法<span style="color: rgb(231, 95, 51);"><strong>漏掉單引號</strong></span>，會發生：An expression contains incompatible data types.</p><pre><code >let ([
~query = "
Select  name, Int ( ( Date" & get(currentDate) & " - birthday ) / 365 ), '歲' 
From contact 
Where addrCity = '新竹市'
"];
executeSql ( ~query ; char(9) ; ""))</code></pre><p><br></p>