# FORM｜健身訓練筆記 — AI 協作規則

這是本專案的開發契約。修改任何檔案前，先閱讀本文件與 README.md；優先遵守使用者當次明確要求。

## 1. 目的與範圍

建立繁體中文的健身學習與訓練筆記網站。使用者可以查動作、收藏、挑選示範菜單、記錄組數與次數，並匯出自己的資料。
重點是可持續擴充的內容系統，不是一次性的網頁展示。網站提供一般運動教育，不提供個人醫療診斷或保證訓練成效。

## 2. 技術與檔案結構

- 純 HTML、CSS、JavaScript，不使用框架、不需 API key、沒有後端。
- `dist/index.html`：語意化頁面、導覽、表單、對話框。
- `dist/assets/styles.css`：設計變數、版面與響應式樣式。
- `dist/assets/data.js`：唯一的動作與菜單內容來源；透過 `window.FORM_DATA` 暴露資料。
- `dist/assets/core.js`：資料驗證、日期與統計的純函式；瀏覽器與 Node 測試共用。
- `dist/assets/app.js`：渲染、搜尋、篩選、收藏、紀錄及匯入匯出。
- `templates/exercise-template.js`：新增動作的格式範本，不直接載入網頁。
- `tests/core.test.cjs`：重要資料行為測試。
- `scripts/serve.cjs`：僅在本機提供預覽的靜態伺服器。
- `.github/workflows/pages.yml`：GitHub Pages 自動部署。
- `docs/assignment.md`：作業設計說明與展示步驟。
- `docs/verification.md`：實際完成的驗證與限制；不得虛構測試結果。

所有檔名使用小寫英文與 kebab-case；內容為 UTF-8。資源連結使用相對路徑，確保 GitHub Pages 子路徑可運作。

## 3. 版型與視覺規則

- 品牌為 FORM，副標「健身訓練筆記」；介面文字使用繁體中文，英文僅作小型輔助標籤。
- 米白底、墨黑文字、橘色重點；顏色統一使用 styles.css 的 CSS variables。
- 最大內容寬度 1180px，保留清楚留白；卡片邊線細，圓角適量，避免大量陰影。
- 主導覽固定三個區域：動作資料庫、訓練菜單、我的紀錄。新增功能先考慮放進既有區域。
- 桌面動作卡三欄、平板兩欄、手機一欄；390px 手機不得水平溢出。
- 每個區域都具備標題、簡介、主要操作與空狀態。
- 所有可操作元素使用 button / a / input / select，禁止以 div 假裝按鈕。
- 表單有 label、鍵盤有清楚 focus-visible、對話框可按 Escape 關閉、尊重 reduced-motion。
- 不加入未授權照片、追蹤碼、外部字型、廣告或新依賴。

## 4. 新增動作的固定格式

只需在 `dist/assets/data.js` 的 exercises 陣列新增一筆，並保持以下欄位：

| 欄位 | 規則 |
| --- | --- |
| id | 唯一且穩定的英文 kebab-case，發布後不可改名 |
| name / english | 繁體中文名稱 / 英文名稱 |
| category | 下肢、胸肩、背部、核心其中之一 |
| equipment | 徒手 或 啞鈴 |
| difficulty | 入門 或 進階控制；不宣稱適合所有人 |
| muscles | 主要訓練部位文字 |
| summary | 一句描述目的，不誇大效果 |
| steps | 3–4 個簡短、可操作的步驟 |
| tips | 2 個技術提醒；避免絕對化姿勢禁令 |
| unit | reps 或 seconds |
| unilateral | 布林值，true 時每側次數與組數需標明 |
| defaultReps | 示範預填值，正整數 |
| source | `{ title, url, checked }`，官方/可信來源與查閱日期 |

新增後搜尋、篩選、詳情、紀錄選單都應自動出現；不要複製整張 HTML 卡片。先查證來源，用自己的話簡述，不整段抄寫。若無法查證，先不要發布該動作。

## 5. 新增菜單的固定格式

菜單放在 plans 陣列，欄位為 id、name、tag、description、note、items。
items 每筆必須含 exerciseId、sets、reps、rest；exerciseId 必須對應既有動作，sets/reps/rest 為正整數，rest 單位秒。
所有菜單明確標示「示範菜單」，不以使用者個資假造個人化處方。
單側動作顯示「每側」，計時動作顯示「秒」，不可把秒數算成重複次數或公斤訓練量。

## 6. 使用者資料與安全

- localStorage key 為 `form-fitness-v1`；結構是 `{ version: 1, favorites: [], records: [] }`。
- 每筆紀錄有 id、date、exerciseId、sets、reps、weight、notes。日期用使用者本機日曆日期，不以 UTC 切日。
- 重量欄位代表單一器材重量（例如單支啞鈴）；徒手與計時動作固定記 0。不要混算總訓練噸數。
- 次數/秒數與組數有界限驗證；JSON 匯入須逐筆驗證格式與引用 ID，任何錯誤拒絕整份匯入。
- 匯入採合併，不清空既有紀錄；重複 id 保留現有版本。新增版本需提供遷移策略。
- 顯示使用者文字使用 textContent 或經統一 escapeHtml；禁止將原始筆記塞入 innerHTML。
- 不把紀錄上傳伺服器。告知使用者紀錄僅儲存在此瀏覽器，可匯出備份。
- 儲存失敗需顯示提示；解析失敗不可立即覆蓋原始儲存內容。
- 刪除紀錄先確認，刪除後提供復原。不可靜默刪除資料。
- 禁止提交帳密、token、真實個人訓練紀錄與測試用個資到 GitHub。

## 7. 每次修改的工作流程

1. 讀本文件與 README，先確認需求屬於內容、樣式還是行為。
2. 優先修改資料層，沿用既有元件與設計變數，避免無關重寫。
3. 若改資料格式，同步更新範本、驗證、測試與文件。
4. 執行 `npm test`；語法檢查已包含在此命令。
5. 執行 `npm start`，開啟輸出的本機網址。驗證搜尋、收藏、動作詳情、菜單帶入、紀錄儲存與重整保留。
6. 改匯入匯出時必須實測備份還原與不合法資料被拒絕。
7. 檢查桌面與 390px 手機、鍵盤操作，以及無資料/無搜尋結果情況。
8. 更新 docs/verification.md，只記錄實際做過的檢查。

## 8. 完成定義

內容有來源、搜尋與所有操作正常、既有紀錄沒有遺失、沒有 console error、檔案規則一致，且 README 對應實際行為。GitHub Pages 部署成功之前不得宣稱「已上線」。

## 9. 後續可直接給 AI 的指令

> 請先閱讀 AGENTS.md。依 exercise-template.js 的格式新增一個「站姿啞鈴彎舉」，查證官方動作來源，沿用既有卡片與篩選邏輯，完成 npm test，並列出修改檔案與檢查結果。

> 請先閱讀 AGENTS.md。使用既有動作新增一份示範菜單，不要更動資料儲存格式，並確認每個 exerciseId 都能開啟詳情與帶入紀錄。
