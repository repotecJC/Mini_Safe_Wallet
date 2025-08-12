Mini Safe Wallet (迷你保險箱錢包)
一個具備存款、白名單提款與每日限額控制的簡易錢包合約。採用 pull 模式提款，並包含基本安全機制（非重入與暫停）。

功能
存款：任何人可向合約轉入 ETH（emit Deposited）
白名單提款：僅白名單地址可提款
每日限額：每位白名單使用者每日提款上限
安全：Checks-Effects-Interactions、nonReentrant、可暫停提款

開發與部署
編譯器：Solidity 0.8.20+
網路：Sepolia 測試網
部署工具：Remix + MetaMask

合約
路徑：Contracts/MiniSafeWallet.sol
已部署地址（部署後填寫）：<待填 Sepolia 地址>

快速開始（Remix）
打開 Remix，加入檔案 contracts/MiniSafeWallet.sol
編譯器設為 0.8.20（或相容）
Deploy & run 選 Injected Provider – MetaMask（Sepolia）
constructor: dailyLimitWei 建議 0.1 ether

部署後：
轉入 0.2 ether（測試存款）
setWhitelist(你的地址, true)
withdraw(0.05 ether) 成功；再提 0.06 失敗（超過日限額）
setWithdrawPaused(true) 後提款失敗；再設回 false 恢復

介面與事件
事件：Deposited, Withdrawn, WhitelistUpdated, DailyLimitUpdated, OwnerChanged, WithdrawPausedUpdated
查詢：contractBalance(), remainingToday(address), withdrawnToday(address)

安全考量
Pull over Push：避免在外部互動中發送資金
非重入：簡易鎖 + CEI 流程
權限：onlyOwner 管理白名單、限額、暫停

路線圖
Week 2：加入前端（React + viem/ethers），事件列表
Week 3：單元測試、Gas 優化、安全檢查清單
Week 4：最終部署與 Demo 錄製

進度標記
v 第0節：環境準備
  第1–3節：存款與查詢
  第4–6節：提款、白名單、日限額、安全
  第8–9節：部署與文件
