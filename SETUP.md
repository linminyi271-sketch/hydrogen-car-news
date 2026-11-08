# 氫能車產業新聞：共用資料庫設定

網站目前以預覽模式運作（`config.js` 的 `API_URL: ''`）。如需讓團隊成員共同讀取新聞、發布 Word 週報、儲存本週重點觀察及保留上傳者紀錄，請設定 Google Apps Script。

## 1. 建立 Google 試算表

1. 使用團隊共用 Google 帳號建立試算表，例如「氫能車產業新聞_資料庫」。
2. 試算表選單：擴充功能 → Apps Script。
3. 將本 Repository 的 `apps-script/Code.gs` 全文貼入編輯器並儲存。
4. 在函式選單選擇 `setup` 並執行，授權後會建立 `news` 與 `observations` 工作表。

## 2. 部署 Apps Script

1. Apps Script 右上角選「部署」→「新增部署作業」。
2. 類型選「網頁應用程式」。
3. 執行身分選「我」；誰可以存取選「所有人」（依組織資安政策調整）。
4. 部署並複製以 `/exec` 結尾的網址。

## 3. 連接網站

1. 開啟 Repository 的 `config.js`。
2. 將 `API_URL: ''` 改成 `API_URL: '剛才複製的 Apps Script 網址'`。
3. 確認 `WEEK_START_DAY: 1` 與後端相同（週一為每期起始日）。
4. Commit 後重新整理 GitHub Pages 網站。

## 4. 每週更新

網站右上角「新增新聞」可選擇：
- 上傳 Word 週報（.docx）
- 貼上週報文字或 JSON
- 單則新增

確認解析結果、區域、日期與標籤後，填寫上傳者並發布。重點觀察可在「本週重點觀察」區塊編輯與儲存。

## 5. 上傳碼（選用）

若需限制上傳者，可在 Apps Script 專案設定的指令碼屬性新增 `UPLOAD_CODE`，並將網站 `config.js` 的 `UPLOAD_CODE_REQUIRED` 設為 `true`。勿將團隊上傳碼寫入公開程式碼。


> **刪除功能更新提醒：** 本次版本新增「刪除選取新聞」與「刪除整期新聞」後，請將 Repository 中最新的 `apps-script/Code.gs` 貼回對應的 Apps Script 專案，儲存後到「部署 → 管理部署作業 → 編輯 → 版本：新版本 → 部署」。原有 `/exec` 網址通常不變。網站 `config.js` 必須設定該後端網址，刪除才會同步到所有使用者；若 `API_URL` 留空，刪除只作用於目前瀏覽器的預覽資料。
