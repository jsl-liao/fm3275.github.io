<h2><span style="color: rgb(0, 0, 0);">executeSql 函數 step by step, 第 4 章，Group 子句</span></h2><p>GROUP BY<span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;"> 子句指定返回的值應按其分組的一個或多個字段的名稱。此子句用於返回一組聚合值。它具有以下格式：</span></p><pre style="text-align: start;"><code>GROUP BY 列 // column</code></pre><p>GROUP BY<span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;"> 子句的範圍是 </span>FROM<span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;"> 子句的表達式。</span></p><p><span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;">因此，</span>columns<span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;"> 指定的列表達式必須來自 </span>FROM<span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;"> 子句中指定的表。</span></p><p><span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;">列表達式可以是以逗號分隔的數據庫表的一個或多個字段的名稱。</span></p><p><span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;">Group 子句和聚合函數一起應用。</span></p><p><span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;">Group 要放在正確的位置，如</span><a href="https://github.com/jsl-liao/fm3275.github.io/blob/main/filemaker%20executeSql%20function/executeSql%20%E5%87%BD%E6%95%B8%20step%20by%20step%2C%20%E7%AC%AC%200%20%E7%AB%A0.md" target="_blank"><span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;">第 0 章所敘述的順序</span></a><span style="color: rgb(51, 51, 51); background-color: rgb(250, 250, 250); font-size: 16px;">。</span></p><p>範例 1:</p><p>從 company 取得每個縣市的公司數, 並組成 json</p><pre><code >While (  
  [    
    ~cityList = ExecuteSQL ( "Select Distinct (addrCity) From company" ; "" ; "");    
    ~end = ValueCount ( ~cityList );    
    ~i = 1 ;    
    ~json = "{}" ;    
    ~endInitial = True  
  ];  
  ~i &lt;= ~end ;  
  [    
    ~city = GetValue (~cityList ; ~i );    
    ~ids = ExecuteSQL ( "Select id From company Where addrCity = ?" ; "" ; "" ; ~city );    
    ~qty = ValueCount(~ids);    ~json = JSONSetElement ( ~json ; ~city ; ~qty ; 2 );    
    ~i = ~i + 1  
  ];  
  substitute ( JSONFormatElements ( ~json ) ; char(9) ; "  "))</code></pre><p>用 Group 子句達成相同的結果</p><pre><code >let (  
  ~json = "{\"" & ExecuteSQL ( "Select addrCity , count(id) From Company Group By addrCity" ; "\":" ; ",\"" ) & "}";  
  substitute ( JSONFormatElements ( ~json ) ; char(9) ; "  "))</code></pre><p>提示:</p><ol><li> json 是<span style="color: rgb(0, 0, 0);">字串</span>資料, 用 column separator 和 row separator 和處理字串的手法, 可以組成 json 資料</li><li><span style="color: rgb(0, 0, 0);">JSONFormatElements 除了提供更好檢視的內容，他還可以加速 data viewer 中 render 資料的速度，尤其在大資料的 &nbsp;json 更明顯。</span></li></ol>