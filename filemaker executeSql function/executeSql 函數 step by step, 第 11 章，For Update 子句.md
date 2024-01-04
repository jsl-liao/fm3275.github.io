<h2><span style="color: rgb(0, 0, 0);">executeSql 函數 step by step,</span><span style="color: rgb(0, 0, 0);"><s> </s></span><span style="color: rgb(0, 0, 0);">第 11 章，For Update 子句</span></h2><p>當資料在編輯的狀態下，鎖住取值的動作，而傳會“?”。鎖住的動作在進入記錄中的任何一個欄位被修改時被啟動，如 onModified。</p><p><span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;">格式為：</span></p><pre><code >For Update [Of column_expressions]</code></pre><p>column_expressions<span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;"> 是您要更新的數據庫表中的字段名列表，由逗號分隔。</span></p><p>column_expressions<span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;"> 是可選的，可以忽略。有寫沒寫不會影醒運算的動作，但可以作為提示作用。</span></p><h3>範例：1</h3><p><span style="color: rgb(0, 0, 0);">在表 contact 的任何一筆是在編輯狀態， 便鎖住取值的動作。</span></p><pre><code >ExecuteSQL ( "
Select name, telAreaCode, telNo 
From contact 
For Update
" ; "" ; "" )</code></pre><h3><span style="color: rgb(0, 0, 0);">範例：2</span></h3><p><span style="color: rgb(0, 0, 0);">在表 contact 的任何一筆 addrCity 是"嘉義市"在編輯狀態， 便鎖住取值的動作。</span></p><p><span style="color: rgb(0, 0, 0);">而在編輯 addrCity 不是"嘉義市"的資料，如台北市、新北市⋯⋯等都不會影響取值的動作。</span></p><pre><code >ExecuteSQL ( "
Select name, telAreaCode, telNo 
From contact 
Where AddrCity = ? 
For Update of telAreaCode
" ; "" ; "" ; "嘉義市")</code></pre><h3><span style="color: rgb(0, 0, 0);">範例：3</span></h3><p><span style="color: rgb(0, 0, 0);">除非康斬的資料是在編輯狀態，其他等都不會影響取值的動作。</span></p><pre><code >ExecuteSQL ( "
Select name, telAreaCode, telNo 
From contact 
Where name = ? 
For Update of telAreaCode
" ; "" ; "" ; "康斬")</code></pre><h3><span style="color: rgb(0, 0, 0);">範例：4</span></h3><p><span style="color: rgb(0, 0, 0);">只有前 10 筆被鎖住。</span></p><pre><code >ExecuteSQL ( "
Select name, telAreaCode, telNo 
From contact 
Where AddrCity = ? 
Fetch 10 Rows Only 
For Update of telAreaCode
" ; "" ; "" ; "苗栗縣")</code></pre><p>提示：前 &nbsp;10 筆並不是你在 FileMaker 看到的前 10 筆。而是依據 sql 排序的前 10 筆。</p>