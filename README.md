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

1. 把 `ai-team-orchestration/` 整個資料夾放到 AI 助手的技能目錄（例如個人用的 `~/.claude/skills/`，或專案裡的 `.claude/skills/`）。
2. 開新對話時說明要用這個技能，例如：「用 ai-team-orchestration 幫我把這個功能做出來」。
3. 它會先確認範圍，再依需要切成 Producer / Dev / QA 三段接手。

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

---

最後更新：2026-10-17
