<h2 style="text-align: start;"><span style="color: rgb(0, 0, 0);">executeSql 函數 step by step, 第 30 章，關係運算子_In</span></h2><p><span style="color: rgb(0, 0, 0);"><strong>In</strong></span><span style="color: rgb(0, 0, 0);"> 搭配 </span><span style="color: rgb(0, 0, 0);"><strong>Where </strong></span><span style="color: rgb(0, 0, 0);">子句用來限定符合表列欄位值為條件（也可以是子查詢所構成的欄位值），來搜尋資料表中的特定資料。</span></p><p><span style="color: rgb(0, 0, 0);"><strong>Not In</strong></span><span style="color: rgb(0, 0, 0);"> 是</span><span style="color: rgb(0, 0, 0);"><strong> In</strong></span><span style="color: rgb(0, 0, 0);"> 的否定形式。</span></p><h3><span style="color: rgb(0, 0, 0);">範例 1： </span></h3><p><span style="color: rgb(0, 0, 0);">在 table: contact 列出 found set 的資料</span></p><pre><code >/*
contact::idList summary field, list of id
cf_listToAnother ( _valueList ; _to_sqlIn_csv_tsv_words_array )
把 filemaker 的 value list 轉成其他格式的資料, 放在 folder: custom function
*/

let (
~vl = cf_listToAnother ( contact::idList ; "sqlIn" );
executeSql ("  Select name, nameEng, gender From contact Where id In (" & ~vl & ")  "; ",  " ; "" ))</code></pre><h3>範例 2：</h3><p>利用子查詢，列出在新北市，公司是以 "材料科技股份有限公司"結尾的員工資料</p><pre><code >executeSql ("Select name, nameEng, gender From contact Where idf In
( Select id From company Where addrCity = '新北市' And name like '%材料科技股份有限公司' )"; ",  " ; "")</code></pre><p><br></p>