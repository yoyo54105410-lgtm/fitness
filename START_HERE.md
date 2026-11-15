# 先看這份：健身訓練筆記作業

## 目前完成的內容

網站程式、AGENTS.md、README、作業說明、動作範本、測試與 GitHub Pages 部署設定都已備齊。
本專案對應公開儲存庫：[yoyo54105410-lgtm/fitness](https://github.com/yoyo54105410-lgtm/fitness)。公開網站的狀態請以 GitHub Actions 部署結果為準。

## 立即看網站

解壓縮後，開啟 `dist/index.html`。
若已安裝 Node.js，建議在專案資料夾執行 `node scripts/serve.cjs`，再開啟 `http://127.0.0.1:4173`。

## 老師最重要的檔案

- `AGENTS.md`：AI 如何理解專案目的、規則、結構與後續開發方式。
- `docs/assignment.md`：設計說明與 2–3 分鐘展示順序。
- `README.md`：執行方式、資料限制、擴充方式與部署教學。
- `docs/verification.md`：哪些功能實際測過、哪些仍待驗證。

## 上傳與公開

1. 使用儲存庫擁有者 `yoyo54105410-lgtm` 登入 GitHub，開啟 `fitness` 儲存庫。
2. 上傳解壓縮後的完整內容到儲存庫根目錄，不要只上傳 ZIP，也不要再多包一層資料夾。
3. 確認根目錄看得到 `AGENTS.md` 和 `.github/workflows/pages.yml`。
4. 進入 **Settings → Pages**，將 **Source** 設為 **GitHub Actions**。
5. 進入 **Actions → Deploy FORM to GitHub Pages → Run workflow**，等工作成功。
6. 回到 **Settings → Pages**，複製 GitHub 顯示的正式網址，並用未登入視窗檢查。

本專案不需要 API key 或付費服務；之後修改 `dist/` 的內容並提交至 main，即可由 workflow 重新發布。

## 最後提交

- GitHub 儲存庫網址。
- 已部署且可公開瀏覽的網站網址。
- 可搭配 `docs/assignment.md` 作為文字說明。

先瀏覽並理解 AGENTS.md，確認你能解釋內容格式與擴充方式，再提交作業。
