executeSql 函數 step by step, 第 6 章，Union 運算子
-------------------------------------------

UNION 運算子將兩個或多個 SELECT 語句的結果合併為一個結果。

結果是 SELECT 語句返回的所有記錄。

默認情況下，不返回重複的記錄。

要返回重複的記錄，使用 ALL 關鍵字 (UNION ALL)。

格式為：

    SELECT statement UNION [ALL] SELECT statement

使用 UNION 運算子時，

1.  每個 SELECT 語句的選擇列表必須具有相同數量的列(field, 欄位)表達式，
2.  以及相同的數據類型，
3.  並且必須按相同的順序指定。

### 範例： 1

取得花蓮縣，台東縣的公司名

    ExecuteSQL ( "
    Select name , addrCity From Company Where addrCity = ?
    Union 
    
    Select name , addrCity From Company Where addrCity = ?
    
    " ; "" ; "" ; "花蓮縣" ; "台東縣")

#### 提示:

1.  對同一個表也可以使用 Union 運算子。
2.  所得的結果，資料的先後順序並不是先花蓮縣再接著台東縣的公司，而是混在一起，由 sql 演算法所決定。

另一種寫法

    ExecuteSQL ( "Select name , addrCity From Company Where addrCity = ? Or addrCity = ?" ; "" ; "" ; "花蓮縣" ; "台東縣")

提示:

和上一種寫法比較，資料的排列順序不同，內含是相同的。如果把兩者 sortValues 可以得到相同的結果。

範例：2

把不同的表的查詢結果 Union 起來

    ExecuteSQL ( "
    Select name , addrCity, addrStr From company Where addrCity = ?
    Union 
    Select addrStr, addrCity, name From contact Where addrCity = ?
     Order By name
    " ; "" ; "" ; "花蓮縣" ; "台東縣")

提示:

1.  sql 會檢查 columns 數量是否相同，依據順序的對應的資料類別是否相同，不管邏輯上的意義。
2.  例子中的計算會組成以三個 column 組成 value 的 value list。
3.  對 Union 之後的資料做排序，Order 子句要寫在 Union 後面。
4.  排序所依據的順序是按照第一個 Select 敘述中的 Column name。