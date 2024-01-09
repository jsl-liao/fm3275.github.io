<h2><span style="color: rgb(0, 0, 0);">executeSql 函數 step by step, 第 17 章，別名（alias）和 As 關鍵字 </span></h2>
<h3><span style="color: rgb(0, 0, 0);">alias 的作用</span></h3>
<ul><li><span style="color: rgb(0, 0, 0);">讓敘述更語易化，更容易理解敘述的含義。</span></li><li><span style="color: rgb(0, 0, 0);">欄位名稱和表名稱都可以使用 alias 。</span></li><li><span style="color: rgb(0, 0, 0);">As 關鍵字可以省略不寫。</span></li><li><span style="color: rgb(0, 0, 0);">在複雜的敘述中，縮短敘述長度，精簡內容。</span></li></ul>
<h3><span style="color: rgb(0, 0, 0);">範例：1</span></h3>
<p style="text-align: start;">這三個寫法的作用完全相同。第二、三種寫法讓敘述內容更語意化。</p>
<p style="text-align: start;">有得有寫 As 有得沒寫 As 並不會影響結果。</p>
<pre><code>let (  [    
~query = "
Select name, nameEng, addrCity, addrStr 
From contact Where addrCity = ?
"];  
ExecuteSql ( ~query ; "" ; "" ; "連江縣" ))</code></pre>
<pre><code>let (  [    
~query = "
Select name chinese_name, nameEng english_name, addrCity city, addrStr street 
From contact Where addrCity = ?
"];  
ExecuteSql ( ~query ; "" ; "" ; "連江縣" ))</code></pre>
<pre><code>let ([
~query = "
Select name As chinese_name, nameEng As english_name, addrCity As city, addrStr As street 
From contact Where addrCity = ?
"];
  
ExecuteSql ( ~query ; "" ; "" ; "連江縣" )
)</code></pre>
<h3>範例：2</h3>
<p style="text-align: start;">這兩個寫法的作用完全相同。第ㄧ種寫法讓敘述內容更精簡。</p>
<p style="text-align: start;">在複雜的敘述中，選擇用完整的寫法或者完全的精簡寫法，不要混用，否則會出錯。</p>
<pre><code>Let ([ 
~query ="
Select y.name, c.name, c.nameEng, c.addrCity, c.addrStr 
From contact C  
Join company Y On C.idf = Y.id    
Where C.addrCity = ? 
Order By C.addrStr, C.name 
" ];
ExecuteSQL ( ~query ; "" ; "" ; "台東縣" )
)</code></pre>
<pre><code>let ([~query ="  
Select company.name, contact.name, contact.nameEng, contact.addrCity, contact.addrStr   
From contact    
Join company On contact.idf = company.id      
Where contact.addrCity = ?   
Order By contact.addrStr, contact.name 
" ];
ExecuteSql ( ~query ; "" ; "" ; "台東縣" ))</code></pre>