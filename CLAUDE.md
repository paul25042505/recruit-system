# RIIMS 專案規則

## 版本號規則
- 版本格式：`X.Y.Z`（定義在 `index.html` 的 `const APP_VERSION="X.Y.Z"`）
- X = 重大改版，Y = 新功能/新頁面，Z = 由 CI 自動遞增（每次 push 到 main）
- 每次完成任務、結束對話前，**直接寫出版本號**，格式：`v2.1.4`（讀取 index.html 中的 APP_VERSION，不加任何說明文字）

## 分支規則
- 開發分支：`claude/connection-failure-K5uxn`
- 部署分支：`main`（GitHub Actions 自動部署到 GitHub Pages）
- 所有修改推送到開發分支，不直接推送 main

## 安全規則
- Firebase service account 私鑰（key_id: `ae1369abeed39c0a1f5e21eea52d3e98abfc1cdc`）絕對不能 commit 或出現在任何程式碼中

## 技術架構
- 單一 HTML 檔案（index.html），無 build step，使用 `const e=React.createElement`
- Firebase Auth 10.12.0 + Firestore 10.12.0（ESM imports via importmap）
- iOS Safari：`position:fixed` 在 `overflow:hidden` flex 容器內會被截斷，批次 view 底部導航使用 `.bnav-inline`（position:relative）
