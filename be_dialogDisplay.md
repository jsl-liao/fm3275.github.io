# BaseElements plugin 介紹_2: be_dialogDisplay

```dotnetcli
be_dialogDisplay(title;message;defaultButton;{cancelButton;alternateButton})
parameters: 
title : the dialog title
message : the content of the dialog
defaultButton : the right most button text, return 1
cancelButton : : 選項, return 2
alternateButton: 選項, return 3
```

它的作用相當於 script 中的 show custom dialog, be_dialogDisplay 是用在 function 中, 是很好用的 function debug tool。

在 data viewer 我們只能看到計算式和計算結果, 無法看到運算的過程, 在適當的位置插入 be_dialogDisplay, 可以讓我們檢驗計算過程產生的數據是否如我們所預料。

範例

```dotnetcli
/*
  • subject:
    check if table name and field names violate sql reserved words
  • format:
    cf_chkNamesBySql
  • parameters:
    none
  • returns:
    value list
  • dependencies: on other cfs, variables, table, fields, scheme or ...
    constant: co_sqlWords
  • version:
    v02
  • date:
    20231213
  • update infomation:
    using filemaker system table: FileMaker_Tables, FileMaker_Fields
  • notes:
    co_sqlWords 從檔案 co_sqlWords.json 取得
  • initial:
    20210708
  • by:
    jeff liao
*/

Let (
  [
    ~baseTableNameList = ExecuteSQL ("SELECT BaseTableName FROM FileMaker_Tables" ; "" ; "");
    ~baseTableNameList = UniqueValues ( ~baseTableNameList );
    ~tableNameList = ExecuteSQL ("SELECT tableName FROM FileMaker_Tables" ; "" ; "");
    ~sqlWordList = JSONListValues ( co_sqlWords; ".");
    /* 在區塊備註前面加上兩條斜線, 前端標示和尾端標示都要加, 可讓備註失效
    ~debug = BE_DialogDisplay(
      "~sqlWordList" ;
      ~sqlWordList ;
      "got it" );
    */
    ~tableNameCheck = FilterValues ( ~tableNameList ; ~sqlWordList );
    ~tableNameCheck = If ( IsEmpty(~tableNameCheck) ;
      "table name check: no violation found";
      "table name check:" & ¶ & FilterValues ( ~tableNameList ; ~sqlWordList ));
    ~fieldNameCheck = 
      While (
        [
          ~i = 1 ;
          ~end = ValueCount ( ~baseTableNameList );
          ~result = ""
        ];
        ~i <= ~end ;
        [
          ~baseTableName = GetValue ( ~baseTableNameList ; ~i );
          ~fieldNameList = ExecuteSQL ( "Select fieldName from filemaker_fields Where tablename =?" ; "" ; "" ; ~baseTableName );
          ~fieldCheck = FilterValues ( ~fieldNameList ; ~sqlWordList ) ;
          /* defaultButton, ~debug = 1 ; cancelButton, ~debug = 2 , alternateButton, ~debug = 3; 用來控制 while loop 怎麼跑
          ~debug = BE_DialogDisplay(
            "~fieldCheck" ;
            ~fieldCheck ;
            "繼續";"到最後"; "退出" );
          ~i = case (
            ~debug = 2 ; ~end - 1 ;
            ~debug = 3 ; ~end ;
            ~i ); 
          */
          ~fieldCheck = If ( IsEmpty(~fieldCheck) ; 
            "field name check on table « " & ~baseTableName & " »: no violation found" ;
            "field name check on table « " & ~baseTableName & " »: violation found as below,¶" & ~fieldCheck );
          ~result = ~result & ~fieldCheck ;
          ~i = ~i + 1
        ];
        ~result
      )
  ];
  ~tableNameCheck & ¶ & ~fieldNameCheck
)

/* return: normal condition
table name check: no violation found
field name check on table « help »: no violation found
field name check on table « dev »: no violation found
*/
```
### 技巧
1. 用區塊備註控制 be_dialogDisplay 作用與否, 在上下備註標示的**前面**都加上**兩條斜線**, 讓 be_dialogDisplay 運作, 把兩條斜線去掉, 使備註恢復作用,  be_dialogDisplay 不運作。這個是寫 function 的基本技巧。
2. 用三個 button 控制 function 怎麼跑。

## 重要
1. 在 debug 完之後 be_dialogDisplay 應該被**備註**或**刪除**, 這不應該出現正常的操作中。我是習慣把它備註起來。
2. 不要把它留在 data viewer 中, 它會證明 data viewer 中的東西會耗用系統資源。 它也會像 noticiations 一樣, 不時提醒你, 它的存在。 

### 參考資料
- https://docs.baseelementsplugin.com/article/502-bedialogdisplay
