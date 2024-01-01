<h2 style="text-align: start;"><span style="color: rgb(0, 0, 0);">executeSql 函數 step by step, 第 28 章，關係運算子_Like</span></h2><p style="text-align: start;"><strong>Like</strong><span style="color: rgb(0, 0, 0);"> 能讓我們依據一個模式 (pattern) 來找出我們要的資料。</span></p><p style="text-align: start;">executeSql 支援的萬用字元</p><table style="width: auto; text-align: start;"><tbody><tr><th colspan="1" rowspan="1" width="auto">萬用字元</th><th colspan="1" rowspan="1" width="auto">意義</th><th colspan="1" rowspan="1" width="auto">範例</th></tr><tr><td colspan="1" rowspan="1" width="auto">%</td><td colspan="1" rowspan="1" width="auto">用來代替「零個」至「多個」字元</td><td colspan="1" rowspan="1" width="auto">'%北%' ：中華民國台北市，台北市，北市，新北市，新北市板橋區，... 都符合。</td></tr><tr><td colspan="1" rowspan="1" width="auto">_</td><td colspan="1" rowspan="1" width="auto">下底線，用來代替「一個」字元</td><td colspan="1" rowspan="1" width="auto">'%北_' ：台北市，新北市，中華民國台北市，...都符合；但是新北市板橋區不符合。</td></tr></tbody></table><h3 style="text-align: start;"><span style="color: rgb(0, 0, 0);">範例 1:</span></h3><pre><code >executeSql ( "
Select name, addrStr, webAddr 
From company 
Where addrCity = '新北市' And name like '%材料科技%'
"; char(9) ; "" )</code></pre><p>找出新北市的公司名稱中含 ”材料科技“ 的公司。</p><h3>範例 2：</h3><pre><code >ExecuteSQL ( "
Select company.name, company.addrCity, contact.name, contact.nameEng 
From contact 
Join company On contact.idf = company.id 
Where company.addrCity = '新北市' And contact.name like '趙_'
"; Char(9) ; "" )</code></pre><p>找出在新北市工作，姓趙，名字是單字。</p>