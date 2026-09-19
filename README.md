# Stylus 自訂樣式

供瀏覽器擴充功能 [Stylus](https://github.com/openstyles/stylus) 使用的自製 UserCSS 樣式。

## Wikipedia Monokai (Wujidadi)

檔案：`wikipedia-monokai-wujidadi.user.css`

套用於 `wikipedia.org` 全站的深色樣式，配色取自 Monokai 與 VS Code 主題 Monokai-Wujidadi。
選擇器結構與 SVG 圖示衍生自 [Wikipedia Catppuccin](https://github.com/catppuccin/userstyles/tree/main/styles/wikipedia)（MIT 授權）。

檔名雖以 `.user.css` 結尾，內容實為 Less，由檔頭的 `@preprocessor less` 交給 Stylus 編譯；
`.user.css` 是 Stylus 安裝器唯一認得的副檔名，不可改成 `.less`。

### 安裝

以下兩種途徑都行不通：

- Stylus 管理頁的「匯入」：Stylus 2.4.11 的「匯入」只接受 JSON 格式的備份檔，無法匯入 `wikipedia-monokai-wujidadi.user.css`。
- 貼進未勾選「as UserCSS」所建立的樣式：傳統（Mozilla 格式）模式不執行 Less，
  會出現「依賴 `@preprocessor` 的程式碼無法運作」警告與 `Unknown word #monokai` 錯誤。

做法一：貼上

1. 在 Stylus 管理頁先勾選「as UserCSS」（以 UserCSS 格式），再按「編寫新樣式」。
2. 全選編輯器內的預設範本並刪除。
3. 貼上 `wikipedia-monokai-wujidadi.user.css` 的全部內容後儲存。

做法二：從本機檔案安裝

1. 在瀏覽器的擴充功能管理頁開啟 Stylus 的「允許存取檔案 URL」。
2. 於網址列開啟 `file:///<本倉庫路徑>/wikipedia-monokai-wujidadi.user.css`。
3. 在 Stylus 安裝頁按「安裝樣式」；勾選「Live reload」後，檔案存檔即自動更新樣式。

若同時裝有 Wikipedia Catppuccin 或其他維基百科樣式，需先停用，避免規則互相覆蓋。

### 設定

安裝後按樣式名稱旁的齒輪可調整：

- 強調色：連結與按鈕的顏色，預設為青色 `#66d9ef`
- 柔和度：前景色向底色 `#272822` 混合的百分比，範圍 0–40，預設 12；0 為 Monokai 原始對比
- 標示重新導向連結：勾選後 `.mw-redirect` 連結顯示為 `#6b99da`

### 驗證

修改後可用 Less 4 編譯檢查語法；
Stylus 的 `@var` 變數需在檔案前自行補上：

```sh
{ printf '@accentColor: sky;\n@highlight-redirect: 0;\n@softness: 12;\n'; cat wikipedia-monokai-wujidadi.user.css; } > /tmp/t.less
npx -y less@4 /tmp/t.less /tmp/out.css
```
