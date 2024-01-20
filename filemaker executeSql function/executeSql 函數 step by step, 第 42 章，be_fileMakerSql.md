<h2>executeSql 函數 step by step, 第 42 章，be<a target="_blank" href="https://docs.baseelementsplugin.com/article/532-befilemakersql" style="border: none; height: 100%;">_</a>fileMakerSql</h2>








<p>be<a target="_blank" href="https://docs.baseelementsplugin.com/article/532-befilemakersql" style="border: none; height: 100%">_</a>fileMakerSql 是 baseElements plugin 提供的函數，可對非目前檔案進行 sql 查詢。</p>




格式: 




<div class="dp-highlighter"><ol start="1" class="dp-sql"><li class="alt"><span><span>be_fileMakerSql ( &nbsp;</span></span>sqlQuery &nbsp;&nbsp;</li><li class="alt">{; &nbsp; columnSeparator&nbsp;; &nbsp; rowSeparator&nbsp;; &nbsp; databaseName&nbsp;; &nbsp; asText&nbsp;; &nbsp; outputPath &nbsp; }&nbsp;) &nbsp;</li></ol></div>










<p>參數 ：&nbsp;</p>










<p>sqlStatement ：要執行的指令。 用法和 executeSql 的 sqlQuery 相同。</p>










<p>columnSeparator （可選）：輸出資料的列分隔符號 - 僅限單一字元。 和 executeSql 不同, 如果輸入 “”，column 的值會連接再一起，不會以“,”分隔。</p>










<p>rowSeparator （可選）：輸出資料的行分隔符號 - 僅限單一字元。&nbsp;<span style="caret-color: rgb(0, 0, 0); font-weight: normal; -webkit-text-size-adjust: auto; text-decoration: none"></span>和 executeSql 不同, 如果輸入 “”，row 的值會連接再一起，不會以“¶”分隔。</p>










<p><span style="caret-color: rgb(0, 0, 0); font-weight: normal; text-align: left; -webkit-text-size-adjust: auto; text-decoration: none">databaseName</span>（可選）：允許您指定除目前資料庫之外的其他<span style="font-weight: bold;">開啟</span>的資料庫。有沒有加副檔名，都接受。&nbsp;</p>










<p>asText（可選）：預設為 True，因為 SQL 會將欄位中的資料作為文字傳回。 檢索單一容器欄位時將其設為 false。&nbsp;</p>










<p>outputPath（可選）：允許您將SQL查詢的結果寫入磁碟。<br /></p>
<p>被查詢的檔案的 sharing -&gt; share with FileMaker Clients 如果設定為 off 則第一次的查詢需要獲得<span style="caret-color: rgb(0, 0, 0); font-weight: normal; -webkit-text-size-adjust: auto; text-decoration: none">被查詢的檔案的同意授權。</span></p>