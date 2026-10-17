# CEO

這是我在 GitHub 上的第一個專案，建立於 2026-10-14。

用來整理與備份我在這裡做的東西，目前以 AI 相關的技能包（skill）為主。

## 什麼是技能包

技能包是一份寫給 AI 助手看的「操作說明書」：把某個工作該怎麼做、有哪些步驟、要注意什麼寫清楚，放進指定資料夾後，AI 就會照著這份說明做事，不用每次重新交代。

## 專案結構

```text
CEO/
├── README.md
└── ai-team-orchestration/          技能包：三個角色接力跑開發流程
    ├── SKILL.md                    主說明與預設工作流程
    └── references/
        ├── project-brief-template.md   專案簡報範本
        ├── sprint-plan-template.md     衝刺計畫範本
        ├── brainstorm-format.md        腦力激盪格式
        └── anti-patterns.md            常見錯誤
```

## ai-team-orchestration

用三個固定的角色接力，把一件開發工作從「想做什麼」推到「做完並驗證」：

| 角色 | 負責什麼 |
|---|---|
| `@ai-team-producer` | 釐清範圍、按規模安排計畫、協調與合併 |
| `@ai-team-dev` | 實作、測試、自我檢查、準備 pull request |
| `@ai-team-qa` | 需要獨立驗證時，實際測行為、回報可重現的問題 |

預設流程：**規劃 → 實作 → 測試 →（視需要）獨立 QA → 合併 → 更新專案狀態**。

流程會依事情大小調整：小改動不必正式規劃；跨檔案或風險高的改動才加 review 或 QA，不做多餘的儀式。

### 檔案說明

| 檔案 | 內容 |
|---|---|
| `SKILL.md` | 主說明：角色分工、預設流程、接手既有專案、交出工作前的收尾 |
| `references/project-brief-template.md` | 專案簡報範本，用來留下跨對話都還用得上的背景 |
| `references/sprint-plan-template.md` | 衝刺計畫範本，給較大的工作列步驟與驗收條件 |
| `references/brainstorm-format.md` | 腦力激盪格式，讓不同觀點互相碰撞後再決定 |
| `references/anti-patterns.md` | 常見錯誤與踩過的坑，簡短條列 |

### 怎麼用

#### 準備

需要一個支援技能（skills）的 AI 助手，例如 Claude Code。技能資料夾放在這幾個位置的其中一個：

| 想給誰用 | 放哪裡 |
|---|---|
| 你自己，所有專案 | Windows：`C:\Users\<你的帳號>\.claude\skills\`<br>macOS / Linux：`~/.claude/skills/` |
| 只有某個專案 | 那個專案根目錄下的 `.claude/skills/` |

`.claude` 是隱藏資料夾，Windows 檔案總管要先把「檢視 → 顯示 → 隱藏項目」打開才看得到。

#### 安裝（第一次）

1. 把這個 repo 下載下來：GitHub 頁面右上角 **Code → Download ZIP**，解壓縮；或用 `git clone`。
2. 找到裡面的 `ai-team-orchestration` 資料夾。
3. 把**整個資料夾**複製到上面選好的 `skills` 目錄裡。
4. 確認路徑長這樣（中間不要多一層）：

   ```text
   .claude/skills/ai-team-orchestration/SKILL.md
   ```

5. 重開一個新的 AI 對話。技能是在開新對話時載入的，舊對話不會自動看到。

#### 開始用

把要做的事講清楚，順便點名這個技能就好：

```text
用 ai-team-orchestration，幫我做一個記帳的小工具
```

它會先當 **Producer** 問清楚範圍與驗收標準，再切到 **Dev** 動手實作，覺得風險高的地方才請 **QA** 獨立驗證。事情小的話它會跳過正式規劃，直接做完。

#### 它會怎麼跑

- **小改動**：不規劃，直接改、直接驗。
- **多步驟或跨檔案**：先產出一份簡短計畫，再開工。
- **風險高、規則多**：加獨立 review 或 QA，確認沒問題才合併。
- **中途被打斷**：把決定的方向、卡住的地方、下一步記在專案文件裡，下次接得上。

#### 常見卡點

| 症狀 | 原因與解法 |
|---|---|
| 講了，AI 沒反應 | 路徑多半多包了一層。要正好是 `skills/ai-team-orchestration/SKILL.md`，不是 `skills/ai-team-orchestration/ai-team-orchestration/SKILL.md` |
| 改了檔案還是沒生效 | 技能在開新對話時載入，重開一個對話 |
| 沒看到三個角色輪流出現 | 這個技能把三個角色寫成「同一個 AI 依序扮演」，不一定會開三個獨立 agent；重點在分工有做到，不在形式 |
| 用中文講也可以嗎 | 可以。技能說明是英文，但你要做什麼用中文講就好 |

## 怎麼維護這個專案

每次改東西都走同一套動作：先看改了什麼，再存檔（commit），最後推上去（push）。

```bash
git status                 # 看哪些檔案被改過
git diff                   # 看實際改了哪幾行
git add -A                 # 把改動加入這次存檔
git commit -m "這次改了什麼"  # 存檔，訊息寫給未來的自己看
git push                   # 推上 GitHub
```

幾個名詞：

- **commit**：一次存檔，會留下一筆紀錄，之後可以回頭看或退回。
- **push**：把本機的存檔送到 GitHub 上。
- **branch**：分支，可以想成「另開一份來改」，確認沒問題再合併回 `main`。

`main` 是主要版本，GitHub 上看到的內容以它為準。

## 修改紀錄

| 日期 | 內容 |
|---|---|
| 2026-10-14 | 建立專案與說明文件 |
| 2026-10-14 | 練習修改 |
| 2026-10-14 | 新增 ai-team-orchestration 技能包 |
| 2026-10-15 | 補回說明文件並加上專案目錄 |
| 2026-10-17 | 補完 README：目錄結構、技能包用法、維護步驟 |
| 2026-10-17 | 把「怎麼用」擴寫成安裝與使用教學 |

---

最後更新：2026-10-17
