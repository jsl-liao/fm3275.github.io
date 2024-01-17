<h2><a href="https://github.com/jsl-liao/fm3275.github.io/blob/main/filemaker%20executeSql%20function/executeSql%20%E5%87%BD%E6%95%B8%20step%20by%20step%2C%20%E7%AC%AC%2003%20%E7%AB%A0%EF%BC%8CWhere%20%E5%AD%90%E5%8F%A5%E8%88%87%E6%AF%94%E8%BC%83%E9%81%8B%E7%AE%97%E5%AD%90.md" target="_blank">executeSql 函數 step by step, 第 03 章，Where 子句與比較運算子</a></h2>


<p>WHERE<span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;"> 子句指定要檢索的記錄必須符合的條件。</span>WHERE<span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;"> 子句包括以下形式的條件：</span></p>


<pre><code>WHERE expr1 rel_operator expr2</code></pre>


<p style="text-align: start;"><code>expr1</code> 和 <code>expr2</code> 可以是字段名稱、常數或表達式。</p>


<p style="text-align: start;"><code>rel_operator</code> 是連結兩個表達式的關係運算子。</p>


<table style="width: 100%; text-align: start;"><tbody><tr><th colspan="1" rowspan="1" width="auto" style="text-align: left;">比較運算子</th><th colspan="1" rowspan="1" width="auto" style="text-align: left;">說明</th></tr><tr><td colspan="1" rowspan="1" width="auto">=</td><td colspan="1" rowspan="1" width="auto">等於</td></tr><tr><td colspan="1" rowspan="1" width="auto">&lt;&gt; 或 !=</td><td colspan="1" rowspan="1" width="auto">不等於，不可以用 FileMaker 的運算符號： ≠</td></tr><tr><td colspan="1" rowspan="1" width="auto">&gt; </td><td colspan="1" rowspan="1" width="auto">大於</td></tr><tr><td colspan="1" rowspan="1" width="auto">&gt;= 或 !&lt;</td><td colspan="1" rowspan="1" width="auto">大於或等於，不可以用 FileMaker 的運算符號： ≥</td></tr><tr><td colspan="1" rowspan="1" width="auto">&lt;</td><td colspan="1" rowspan="1" width="auto">小於</td></tr><tr><td colspan="1" rowspan="1" width="auto">&lt;= 或 !&gt;</td><td colspan="1" rowspan="1" width="auto">小於或等於，不可以用 FileMaker 的運算符號： ≤</td></tr></tbody></table>


<p style="text-align: start;">executeSql 的比較運算子只能用於 Where 子句。</p>


<p style="text-align: start;">必須是相同的 type 的資料之間才能做運算。</p>


<p style="text-align: start;">只使用 = 比使用 &gt;, &lt;, &gt;=, &lt;= 的運算速度快。</p>


<h3>範例 1: </h3>


<p>找出英文名字是以 "T"或 “T”以後的字母開頭的姓名和英文名字</p>


<pre><code>ExecuteSQL ( "Select name, nameEng From contact Where nameEng &gt;= 'T'" ; "" ; "")</code></pre>


<p>比較的值是區分大小寫的，如果<span style="color: rgb(0, 0, 0);">'T'</span>寫成<span style="color: rgb(0, 0, 0);">'t'</span>，可能會找不到資料，因為習慣上名字的第一個字母會用大寫。ASCII 小寫字母排在大寫字母後面。</p>
<div class="dp-highlighter"><ol start="1" class="dp-sql"><li class="alt"><span><span>ExecuteSQL&nbsp;(&nbsp;"&nbsp;&nbsp;</span></span></li><li class=""><span><span class="keyword">Select</span><span>&nbsp;</span><span class="keyword">name</span><span>,&nbsp;nameEng&nbsp;&nbsp;&nbsp;</span></span></li><li class="alt"><span><span class="keyword">From</span><span>&nbsp;contact&nbsp;&nbsp;&nbsp;</span></span></li><li class=""><span><span class="keyword">Where</span><span>&nbsp;nameEng&nbsp;&gt;=&nbsp;</span><span class="string">'t'</span><span>&nbsp;&nbsp;</span></span></li><li class="alt"><span><span class="string">"&nbsp;;&nbsp;"</span><span class="string">"&nbsp;;&nbsp;"</span><span>") &nbsp;</span></span></li></ol></div>


<h3><span style="color: rgb(0, 0, 0);">範例 2: </span></h3>


<p><span style="color: rgb(0, 0, 0);">找出住址在花蓮縣“且”是女性的人的名字和 email</span></p>
<div class="dp-highlighter"><ol start="1" class="dp-sql"><li class="alt"><span><span>ExecuteSQL&nbsp;(&nbsp;"&nbsp;&nbsp;</span></span></li><li class=""><span><span class="keyword">Select</span><span>&nbsp;</span><span class="keyword">name</span><span>,&nbsp;email&nbsp;&nbsp;&nbsp;</span></span></li><li class="alt"><span><span class="keyword">From</span><span>&nbsp;contact&nbsp;&nbsp;&nbsp;</span></span></li><li class=""><span><span class="keyword">Where</span><span>&nbsp;addrCity&nbsp;=</span><span class="string">'花蓮縣'</span><span>&nbsp;</span><span class="op">and</span><span>&nbsp;&nbsp;gender=</span><span class="string">'女'</span><span>&nbsp;&nbsp;</span></span></li><li class="alt"><span><span class="string">"&nbsp;;&nbsp;"</span><span class="string">"&nbsp;;&nbsp;"</span><span>") &nbsp;</span></span></li></ol></div>


<p>Where 可以用 And （且），Or（或）進行多重條件的資料過濾。</p>


<h3><span style="color: rgb(0, 0, 0);">範例 3: </span></h3>


<p><span style="color: rgb(0, 0, 0);">找出住址在花蓮縣“且”是女性 或者是住址在台東縣“且”是女性的人的名字和 email</span></p>
<div class="dp-highlighter"><ol start="1" class="dp-sql"><li class="alt"><span><span>ExecuteSQL&nbsp;(&nbsp;"&nbsp;&nbsp;</span></span></li><li class=""><span><span class="keyword">Select</span><span>&nbsp;</span><span class="keyword">name</span><span>,&nbsp;email&nbsp;&nbsp;&nbsp;</span></span></li><li class="alt"><span><span class="keyword">From</span><span>&nbsp;contact&nbsp;&nbsp;&nbsp;</span></span></li><li class=""><span><span class="keyword">Where</span><span>&nbsp;(&nbsp;addrCity&nbsp;=</span><span class="string">'花蓮縣'</span><span>&nbsp;</span><span class="op">and</span><span>&nbsp;gender=</span><span class="string">'女'</span><span>&nbsp;)&nbsp;</span><span class="op">OR</span><span>&nbsp;(&nbsp;addrCity&nbsp;=</span><span class="string">'台東縣'</span><span>&nbsp;</span><span class="op">and</span><span>&nbsp;gender=</span><span class="string">'女'</span><span>&nbsp;)&nbsp;&nbsp;</span></span></li><li class="alt"><span><span class="string">"&nbsp;;&nbsp;"</span><span class="string">"&nbsp;;&nbsp;"</span><span>") &nbsp;</span></span></li></ol></div>


<p>多重的過濾條件可以用（）來加以組合</p>