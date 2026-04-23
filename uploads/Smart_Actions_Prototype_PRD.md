# Logi Options+ Smart Actions — Redesign Prototype PRD
> 互動原型規格書｜給 Claude Design 製作用
> 作者：Terry Wu｜日期：2026-04-19

---

## 1. 專案概述

### 這是什麼
一個互動式原型，展示重新設計後的 Logi Options+ Smart Actions 體驗。這個原型會被連結在投遞 Logitech Senior UX Designer（Personal Workspace Solutions 團隊）的求職簡報中。

### 要產出什麼
一個產出：**可點擊的互動原型**（React artifact 或 HTML），展示完整的 Smart Actions 重新設計體驗。它應該要像一個真實的產品 redesign，不是抽象的 wireframe。

### 設計調性
看起來要像真正的 Logitech Options+ 介面。參考實際產品的深色 UI 風格（見 `Lift_3.png` 和 `logitech11.PNG`）。專業、精緻、有觀點。

---

## 2. 背景：現有體驗的問題

這次 redesign 解決的是透過親身使用 Logitech Lift 滑鼠上的 Smart Actions 所發現的兩個核心問題：

### 問題一 — 範本與使用者的真實環境脫節
- 範本用的是 Logitech 的通用假設（例如「工作模式」預設開 Word、Excel、PowerPoint），而不是使用者電腦上實際安裝的軟體
- 使用者必須點進範本才能發現內容不相關——主頁卡片不預覽動作序列的內容
- Smart Actions 只能啟動本機應用程式——Google Meet 之類的瀏覽器工具完全不支援

### 問題二 — 建立工具說的是系統語言，不是使用者語言
- 「新增動作」選單顯示的是工程零件（應用程式、按鍵敲擊、文字、系統、延遲），不是使用者的目標
- 步驟用系統指令呈現（「移到前景 Chrome → 3 延遲秒數 → 新瀏覽器標籤 → 貼上 → 按鍵敲擊: Enter」），而不是結果（「打開 Chrome → 前往 Gmail」）
- 點擊步驟想換 app，結果系統卻打開那個 app 的動作選單——使用者的意圖和系統的回應方向完全相反

### 解決方案：
1. **個人化範本引擎** — 掃描使用者已安裝的 app + 詢問工作角色 → 生成相關範本
2. **AI 自然語言建立** — 讓使用者用自己的話描述想做的事 → AI 組裝動作序列

---

## 3. 參考截圖

只需要兩張截圖作為視覺參考，不要嵌入到原型中。

| 檔案 | 用途 |
|------|------|
| `logitech11.PNG` | **起始畫面參考。** Options+ 首頁——深色背景，左上角「Good Afternoon」問候語，中央 Lift 滑鼠 3D 渲染圖，右上角有 icon 按鈕和使用者名稱「Terry」。 |
| `Lift_3.png` | **Smart Actions 頁面參考。** 現有 SA 主頁——左側選單（Templates/Manage）、頂部導航（搜尋、匯入、+ 建立）、分類 tabs、卡片網格。 |

不要把截圖嵌入原型中。它們是深色 UI 風格、佈局結構和間距的參考。原型展示的是**重新設計後的新體驗**。

---

## 4. 原型流程

### Flow 0 — Options+ 首頁（起始畫面）

原型從這裡開始——不是直接進入 Smart Actions。這讓體驗錨定在真實的產品情境中。

**佈局參考：** `logitech11.PNG`

- 深色背景
- 左上角：問候語（「Good Afternoon」）
- 右上角導航：「+ ADD DEVICE」按鈕，接著是 icon 按鈕群，然後是使用者名稱「Terry」和設定齒輪 icon
- 中央：Logitech Lift 垂直滑鼠 3D 渲染圖，下方電量指示（100%）
- **關鍵元素：** 右上角導航區的 Smart Actions icon（✦）。首次造訪時，它會彈出一個 tooltip/popover 提示：**「Try Smart Actions」**——這是通往 onboarding 流程的入口。

**互動：** 點擊 Smart Actions icon 或「Try Smart Actions」提示，進入 Flow A（首次 onboarding）。

---

### Flow A — 首次 onboarding

使用者第一次打開 Smart Actions 時，會先看到 onboarding 流程，然後才進入主頁。

**Step 1 — 歡迎 & 掃描**
- 置中佈局，有 Smart Actions 品牌元素
- 說明文案：「We'll scan your installed apps to create templates that match your actual workflow. No generic setups — just what's relevant to you.」
- 主要 CTA：「Scan my apps」
- 小字隱私說明：「We only read app names. No data is collected.」

**Step 2 — 確認常用 app**
- 掃描結果以 app icon + 名稱的網格呈現
- 要顯示的 app：Chrome, Figma, Spotify, LINE, Zoom, Edge, Notion, Adobe Acrobat, Battle.net, Notepad, Settings, Snipping Tool
- 部分預設已選（Chrome, Figma, Spotify, Zoom, Notion）
- 使用者可以切換每個 app 的選取狀態
- 指示文案：「Select the ones you use daily.」

**Step 3 — 選擇工作角色**
- 「What best describes your work?」
- 三個選項，單選：
  - **Designer** — 「Figma, creative tools, visual work」
  - **Developer** — 「Code editors, terminals, repos」
  - **General office** — 「Docs, email, meetings」
- 這決定了系統會生成哪些範本組合
- CTA：「Generate my templates」（選擇角色後才啟用）

**Step 4 — 過渡到個人化主頁**

**進度指示：** 整個 onboarding 過程中顯示 3 步進度條。

---

### Flow B — 個人化主頁

Onboarding 完成後，使用者看到重新設計的 Smart Actions 主頁。

**佈局參考：** 參照 `Lift_3.png` 的整體結構——左側選單、頂部導航、卡片內容區。但有以下改變：

**頂部導航：**
- 返回箭頭 +「Smart Actions」標題
- 搜尋框
- Import 按鈕
- 「+ Create」按鈕（打開 AI builder）

**左側選單：**
- Templates（active）
- Manage

**內容區 — 頂部：**
- AI 輸入框顯著放置：「Tell me what you want to automate...」加上送出箭頭
- 點擊後打開 AI builder（Flow C）

**內容區 — 範本卡片：**
- 分類 tabs：All, Productivity, Meeting, AI, Leisure, For designers, For developers
- 排序下拉選單（例如「Most recent」）
- 卡片網格（3 欄）

**每張範本卡片應該顯示：**
- 頂部一排 app icon（代表涉及哪些 app）
- 範本名稱（例如「Design mode」、「Meeting prep」、「Break time」）
- **步驟結果預覽** — 這是跟現有設計最關鍵的差異。每張卡片用白話文顯示動作會做什麼：
  - 「1. Open Figma」
  - 「2. Open Chrome」
  - 「3. Play Spotify」
- 分類標籤（Productivity / Leisure）
- 底部「+ Add」動作

**範本範例（假設選了 Designer 角色，常用 app 為 Chrome, Figma, Spotify, Zoom, Notion）：**

| 名稱 | 步驟 | 標籤 |
|------|------|------|
| Design mode | 1. Open Figma → 2. Open Chrome → 3. Play Spotify | Productivity |
| Meeting prep | 1. Open Zoom → 2. Open Notion | Productivity |
| Break time | 1. Chrome → YouTube → 2. Play Spotify | Leisure |
| Research mode | 1. Open Chrome → 2. Open Figma → 3. Open Notion | Productivity |
| Music + browse | 1. Play Spotify → 2. Open Chrome | Leisure |
| Design review | 1. Open Zoom → 2. Open Figma → 3. Open Chrome | Productivity |

**額外元素：**
- 「Rescan apps」按鈕放在容易找到的位置（例如頂部附近）

---

### Flow C — AI 自然語言建立

點擊主頁的 AI 輸入框或「+ Create」按鈕觸發。

**打開一個全螢幕（或 overlay）的對話視窗。**

**歡迎狀態（使用者還沒輸入任何東西時）：**
- icon / 視覺元素
- 問候語：「What would you like to automate?」
- 副標：「Describe a task you repeat often — I'll build a Smart Action for you. No technical knowledge needed.」
- 3 個可點擊的建議卡片：
  - 「Prepare for a meeting — open video call + notes app」
  - 「Start my work session — open all my daily tools」
  - 「Take a break — open entertainment and music」
- 底部固定輸入框：「Describe what you want to automate...」

**對話流程（使用者輸入或點擊建議後）：**

原型應該模擬這段特定對話：

1. **使用者訊息：** 「Before my meeting, open Google Meet with camera and mic off, then open Notion for notes」

2. **AI 回應：** 「Got it! I'll set that up. Let me confirm a few details:」

3. **AI 提問：** 「Which browser do you use for Google Meet?」
   - 可點擊的選項：Chrome / Edge / Other

4. **使用者選擇：** Chrome

5. **AI 回應：** 「Chrome — noted.」

6. **AI 提問：** 「Which app for notes?」
   - 可點擊的選項：Notion / Notepad / Other

7. **使用者選擇：** Notion

8. **AI 回應：** 「Perfect — your Smart Action is ready.」

9. **過渡到結果頁面**

**結果頁面：**
- 結果卡片，cyan 邊框，顯示：
  - 標題：「Meeting prep」
  - 步驟用結果語言呈現：
    - 1. Open Chrome → Google Meet
    - 2. Turn off camera
    - 3. Turn off microphone
    - 4. Open Notion

- **觸發器選擇器：** 「Trigger: Select a button ▾」
  - 點擊循環切換：「Lift — Middle button」→「Lift — Forward button」→「Keyboard shortcut: Ctrl+Shift+M」

- **修改輸入框：** 「Want to change something? Tell me...」——表示修改也是透過對話完成

- **動作按鈕：**
  - 「Try it」— 點擊顯示回饋：「Running... Chrome → Google Meet → Camera off → Mic off → Notion opened. Looks good!」
  - 「Save」— 點擊顯示回饋：「Saved! 'Meeting prep' is now active. Press your trigger to use it anytime.」

- **進階連結：** 「Advanced: edit steps manually」——小字、弱化呈現。存在但不是主要路徑。

---

## 5. 互動細節

| 元素 | 行為 |
|------|------|
| App 選擇 chips（onboarding） | 點擊切換選取/取消選取 |
| 角色卡片（onboarding） | 單選——點擊一個會取消其他 |
| 「Generate my templates」按鈕 | 未選角色時 disabled（灰化） |
| AI 建議卡片 | 點擊後填入輸入框並自動送出 |
| AI 選項 chips | 點擊一個後其他變暗，新增使用者訊息，推進對話 |
| 觸發器選擇器 | 每次點擊循環切換選項 |
| 「Try it」按鈕 | 顯示成功回饋訊息 |
| 「Save」按鈕 | 顯示確認訊息 |
| 返回按鈕 | 導航到前一個畫面 |

---

## 6. 設計自由度

這份 PRD 定義的是原型中**該有什麼**和**該怎麼運作**。原型設計師應該用自己的判斷來決定：

- 佈局比例和間距
- 視覺層級和字體排版
- 動畫和轉場
- 微互動和 hover 狀態
- onboarding → 主頁 → AI builder 之間的轉場方式
- AI builder 要用全螢幕、overlay、還是側面板
- icon 和插圖的選擇
- 任何能讓體驗更真實的額外打磨

目標是一個讓人覺得**可信、精緻的產品 redesign 原型**——不是 wireframe，也不是現有 UI 的像素級複製品。

---

*文件結束*
