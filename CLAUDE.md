# RIIMS 專案規則

## 版本號規則
- 版本格式：`X.Y.Z`（定義在 `index.html` 的 `const APP_VERSION="X.Y.Z"`）
- X = 重大改版，Y = 新功能/新頁面，Z = 由 CI 自動遞增（每次 merge 到 main 觸發 GitHub Actions）
- **每次完成任務、結束對話前**：執行 `git fetch origin main && git show origin/main:index.html | grep -o 'APP_VERSION="[^"]*"'` 取得 main 上的實際版本，再直接寫出，格式：`v2.1.4`（不加任何說明文字）
- 注意：dev branch 的版本比 main 少一號，因為 CI merge 後才自動遞增 Z，**務必讀 origin/main 的版本**

## 分支規則
- 開發分支：`claude/connection-failure-K5uxn`
- 部署分支：`main`（GitHub Actions 自動部署到 GitHub Pages）
- 所有修改推送到開發分支，完成後立即用 GitHub MCP 工具建立 PR 並 merge 到 main（使用 squash merge）
- 若 merge 衝突：`git fetch origin main && git rebase origin/main && git push --force-with-lease`，再重新 merge

## 討論優先規則
- 當使用者說「來討論」、「我們討論一下」、「先討論」、「討論看看」或任何帶有「討論」語意的話，**絕對不能直接寫程式碼**
- 必須先討論並雙方同意架構、方向、實作方式後，才能開始動手寫程式
- 討論階段只用文字說明，不產出任何程式碼片段，直到使用者明確說「好」、「開始」、「來做」、「繼續」之類的確認語

## 安全規則
- Firebase service account 私鑰（key_id: `ae1369abeed39c0a1f5e21eea52d3e98abfc1cdc`）絕對不能 commit 或出現在任何程式碼中

## 技術架構
- 單一 HTML 檔案（index.html），無 build step，使用 `const e=React.createElement`
- Firebase Auth 10.12.0 + Firestore 10.12.0（ESM imports via importmap）
- iOS Safari：`position:fixed` 在 `overflow:hidden` flex 容器內會被截斷，批次 view 底部導航使用 `.bnav-inline`（position:relative）
