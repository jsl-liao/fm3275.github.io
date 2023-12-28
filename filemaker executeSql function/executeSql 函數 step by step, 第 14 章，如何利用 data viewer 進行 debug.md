executeSql 函數 step by step, 第 14 章，如何利用 data viewer 進行 debug
------------------------------------------------------------

1.  在 data viewer 的 expression 區域輸入executeSql 計算式，如果有錯誤，result 只會顯示“?“，只能得知發生錯誤，卻不知道發生了什麼錯誤。
2.  不要失望，點擊 monitor，關閉 expression 顯示。
3.  再次雙擊計算式，在 result 區域會顯示關於錯誤狀況的敘述。
4.  檢查 Select 敘述只要發現有錯誤，就會終止敘述的解譯，如果敘述有多個錯誤，需要重複上述的動作數次才能完成 debug。
5.  個人的經驗：只有在極少數的狀況下，不會顯示關於錯誤的敘述。