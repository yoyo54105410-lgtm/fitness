# FORM｜健身訓練筆記

**把每一次練習，變成看得見的進步。**

原始碼：[yoyo54105410-lgtm/fitness](https://github.com/yoyo54105410-lgtm/fitness)。
網站採用 GitHub Pages；發布狀態請見 [Actions](https://github.com/yoyo54105410-lgtm/fitness/actions) 與 [Pages 設定](https://github.com/yoyo54105410-lgtm/fitness/settings/pages)。

這是一個以 `AGENTS.md` 作為 AI 開發契約的靜態網站。核心是用固定內容格式與一致版型，讓未來新增動作、菜單時不必重寫頁面。

## 專案內容

- 6 個動作：徒手深蹲、跪姿伏地挺身、單臂啞鈴划船、臀橋、鳥狗式、前臂平板支撐。
- 部位篩選、關鍵字搜尋、收藏，以及有步驟與來源的動作詳情。
- 3 份明確標示為示範的訓練菜單，可將每個動作帶入紀錄表單。
- 日期、組數、次數或秒數、單支器材重量、心得紀錄。
- 本機儲存、JSON 匯出／合併匯入、刪除確認與短時間復原。
- 手機與桌面響應式版面、鍵盤操作與空狀態。

## 本機執行

安裝 Node.js 18 以上版本後，在專案根目錄執行：

```bash
npm start
```

開啟終端機顯示的 `http://127.0.0.1:4173`。不需 `npm install`，本專案沒有套件依賴。
若系統沒有 npm，也可直接執行 `node scripts/serve.cjs`。
直接雙擊 `dist/index.html` 可以瀏覽；為了固定瀏覽器儲存範圍與測試，建議使用上述本機伺服器。

## 檢查

```bash
npm test
```

包含 JavaScript 語法檢查，以及內容引用、備份還原、格式驗證、合併去重、日期統計測試。
無 npm 時依序執行：

```bash
node --check dist/assets/data.js
node --check dist/assets/core.js
node --check dist/assets/app.js
node tests/core.test.cjs
```

瀏覽器操作結果與限制請見 [驗證紀錄](docs/verification.md)。

## 讓 AI 繼續擴充

1. 先讓 AI 閱讀 [AGENTS.md](AGENTS.md)。
2. 動作內容統一放在 `dist/assets/data.js`；可複製 [動作範本](templates/exercise-template.js)。
3. 菜單以 `exerciseId` 引用動作；不要複製動作文字或卡片 HTML。
4. 通過檢查後，再提交修改與部署。

範例指令：

> 請依 AGENTS.md 新增一個「站姿啞鈴彎舉」。沿用既有資料格式與卡片版型，查證動作來源，確認搜尋、收藏與紀錄選單都正常，不要修改現有 localStorage 結構。

## GitHub 與 GitHub Pages

1. 本專案的公開儲存庫為 `yoyo54105410-lgtm/fitness`。若要複製專案，可先建立自己的公開儲存庫。
2. 上傳完整專案，包含根目錄 `AGENTS.md`、`README.md`、`dist/`、`docs/`、`tests/`、`scripts/`、`templates/` 與 `.github/workflows/pages.yml`。不要只上傳壓縮檔。
3. 在儲存庫 **Settings → Pages → Build and deployment → Source** 選擇 **GitHub Actions**。
4. 進入 **Actions → Deploy FORM to GitHub Pages → Run workflow**。也可以設定完成後再 push 到 `main` 觸發部署。
5. workflow 成功後，到 Settings → Pages 取得網站連結。本專案預期網址為 `https://yoyo54105410-lgtm.github.io/fitness/`；成功部署前不代表已上線，請以 GitHub 顯示結果為準。

已附 Pages workflow，部署的是 `dist/`。所有靜態資源使用相對路徑，因此可在儲存庫子路徑運作。

## 資料與限制

- 訓練紀錄僅存在目前瀏覽器、目前網站網址下的 localStorage，不會傳至伺服器，也不會跨裝置同步。
- 本機網址、預覽網站、GitHub Pages 是不同網站，資料不會自動共用；請使用匯出與匯入移轉。
- 瀏覽器無痕模式、清除網站資料或換瀏覽器可能讓紀錄消失；請定期備份。
- 匯入只接受本網站 v1 格式，逐筆驗證後合併；重複 id 保留現有版本，不覆蓋筆記。
- 同一筆紀錄代表相同重量與次數的多組；若各組不同，請分開記錄。
- 單側動作的組數與次數皆以每側記錄，啞鈴重量為單支重量；平板支撐以秒計，不計算總公斤訓練量。
- 示範菜單不是個人化處方，內容不替代教練現場指導或醫療建議。

## 資料來源與製作

動作摘要以自己的話整理自 [ACE Exercise Library](https://www.acefitness.org/resources/everyone/exercise-library/)，每個動作附原始網址與查閱日期。示範菜單是本專案自訂範例，並非 ACE 推薦處方。
頁面標誌與圖形為專案原創 SVG/CSS，未使用第三方照片或追蹤服務。
本專案在使用者選定主題後，由 AI 協助撰寫規則、程式、文件並驗證。

完整作業敘述請見 [docs/assignment.md](docs/assignment.md)。
