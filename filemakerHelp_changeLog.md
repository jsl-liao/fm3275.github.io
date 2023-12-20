## v.04
> date: 2023/12/21

revision:
1. 打開 app 先取得 get(systemLanguage) 的內容，並依此來設定導航欄的按鍵的顯示，及提示的顯示。
如果取得的是 traditional chinese，會以繁體中文顯示；如果是 simplfied chinese 會以簡體中文顯示；如果是其他語言，則會以英文顯示。
2. bug fix
## v.031
> date: 2023/12/16
1. 加入 Claris FileMaker 19 Data API Guide
1. 修正在翻成繁體中文後, 在切換到簡體中文, 無法切換的 bug
## v.03
> date: 2023/12/14
### 整合以下 help 網站: 
1. Claris Pro and FileMaker Pro Help
1. Claris FileMaker Pro 19 Help
1. Claris FileMaker Security Guide
1. Claris Go and FileMaker Go Help
1. Claris FileMaker SQL Reference
1. Claris Studio
1. Claris FileMaker WebDirect Guide 
1. Claris Data API and FileMaker Data API Guide
1. Claris FileMaker Cloud Help
1. Claris Server and FileMaker Server Help
1. Claris Connect Help

###### 並不是每個網站都有翻譯成繁體中文的功能，如果網站沒有此功能，按鍵不會出現。
###### 記錄你離開網站的頁面，下一次切換到這個網站，會回到上一次離開這個網站時的頁面。
###### 重置按鍵使系統恢復到出廠設定，頁面到 Claris Pro and FileMaker Pro Help 首頁。當遇到狀況異常時，可點擊此鍵。

### v.02
> date:2023/12/10

1. 新增一個 button 以關鍵字進行 browser 的 google search。
按下時如果同時按下輔助鍵, 則會只查詢 Claris 的網站; 
如果只是點擊則是進行一般的 google search; 
如果未輸入關鍵字, 則會打開 google search 的頁面。
2. 列印的 button 在 web viewer 沒有作用, 在繁體中文的模式下刪除。
3. 加上顯示 change log 的 button。
4. 修改了幾個詞的翻譯。

### v.01
> date: 2023/12/07

first release