# BaseElements plugin 介紹_1: be_regularExpression

```dotnetcli
be_regularExpression ( text ; expression {; options ; replaceString } )
parameters: 
text: 要處理的字串
expression: 字串形式的正則表示式 (pattern)
options: 選項 (modifier, flag)
replaceString: 要用來取代符合 RegExp 的文字
```

regular expression: 有人翻做"正規表示式", 有人翻作"正則表示式"。有人形容的很好, 她很簡單, 簡單到令人看不懂。其實要搞懂它, 真的不容易, 但是要用它卻不是太難。因為我們平常會用的處理方式在網路上都可以找到範本。以下會講怎麼找。 中文也可以用, 但是, 很複雜很麻煩, 我是不會去找麻煩的。

參數中需要說明的只有兩個: expression,和 options
expression: 表達字串的內容長的樣子, 而不是字串的內容。請參考以下網頁。
options: 可以用的有三個 "g" "m" "i", 不分先後順序。

g: global, 處理內容包含整個要處理的字串, 如果不寫, 表示只要找到第一個就下課, 不繼續找下去。
m: multiline, 把每一行都當作要處理的標的。如果只有寫 "m" 沒有寫 "g", 哪只有第一行會被處理。
i: case insentive, 不需分大小寫。有寫沒寫。

範例

```dotnetcli
// 我要取得 web viewer 網頁的語系識別碼, 但不知道在什麼位置, 是大寫還是小寫, 只知道他長這個樣子: "/xx/"
let (
  ~text = GetLayoutObjectAttribute ( "wv_main" ; "source");
  // "https://help.claris.com/en/pro-help/content/arranging-objects.html";
  be_regularExpression ( ~text ; "\/\w{2}\/", "i" )
)

// 取得: /en/
// 如果要把換成簡體中文的網頁網址
// be_regularExpression ( ~text ; "\/\w{2}\/"; "i" ; "/zh/")
// 取得: "https://help.claris.com/zh/pro-help/content/arranging-objects.html"
```

如果用 FileMaker 的函數去寫, 就比較麻煩, 前綴有可能是不一樣的

```dotnetcli
let ( 
  [ 
    ~text = GetLayoutObjectAttribute ( "wv_main" ; "source");
    ~prefix = "https://help.claris.com/" ;
    ~lenText = length(~text);
    ~lenPrefix = length(~prefix)
  ];
  right ( left ( ~text ; ~lenPrefix + 2 ) ; 2 )
)
```

v19 的 help 長這個樣字

[https://help.claris.com/archive/fm19/en/pro-help/content/index.html]

如果套用上面計算式, 會得到錯誤的結果,
用 regExp 則不用考慮這個問題

## 如何找 RegExp 的範例

RegExp 最常用的是用來檢查格式是否符合
如果你要找檢查 url, 在 查詢 輸入 regexp url 或 regex url
如果你要找檢查 電話號碼, 在 查詢 輸入 regexp 電話號碼 或 regex 電話號碼
你可能看到類似像被兩條斜線包起來

regex = /a/; 相當於 regex = 'a'
regex = /a/,'gmi'; 相當於 regex = ('a','gmi')

常伴隨出現的 javascript method 有 regex.test , regex.exec 或 string.match , string.replace

### 可以參考以下網站的介紹

- https://www.fooish.com/regex-regular-expression/
- https://www.w3schools.com/jsref/jsref_obj_regexp.asp
