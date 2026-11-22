# 論文工作台 skill

讓 Codex、Claude（Cowork／桌面版／Claude Code）會用[論文工作台](https://thesis.pwlee.xyz)：整理文獻、設計問卷、處理指導教授的意見、寫論文章節。

最簡單的方法：登入論文工作台 → 左邊「連接 Claude」→ 複製「帶我設定」那段話，貼給你的 Codex 或 Claude，它會一步一步帶你做完。

## Claude Cowork／桌面版

1. Customize → Plugins → Add → Add marketplace → Add from a repository，輸入 `leepoweii/thesis-workbench-skills`。
2. 在 Plugins 裡安裝 `thesis-workbench`。
3. Customize → Connectors，確認「thesis-workbench」已連上；第一次用時會請你用 Google 登入論文工作台（用你登入網站的同一個 Gmail），按「允許」。
   如果沒有自動出現：Customize → Connectors → + Add → Add custom connector，網址填 `https://thesis.pwlee.xyz/mcp`；驗證設定那頁兩個都維持預設（Sign in now、Use Claude's published identity），捲到最下面按 Add。出錯的話 OAuth client 改選 Register automatically。

## Codex

1. 跟 Codex 說：「用 skill-installer 從 GitHub 的 leepoweii/thesis-workbench-skills 安裝 plugins/thesis-workbench/skills/thesis-workbench」。
2. 加連接器：`codex mcp add thesis-workbench --url https://thesis.pwlee.xyz/mcp`，再 `codex mcp login thesis-workbench` 用 Google 登入。
   Codex 桌面版也可以：Settings → MCP servers → Add server → Streamable HTTP，貼上網址 → Save → Authenticate。

## Claude Code

```
/plugin marketplace add leepoweii/thesis-workbench-skills
/plugin install thesis-workbench@thesis-workbench
```
然後 `/mcp` 選 thesis-workbench 登入。

## claude.ai 網頁版

Customize → Skills → + → Create skill → Upload a skill，上傳論文工作台「連接 Claude」頁下載的壓縮檔；連接器在 Customize → Connectors 加。

---

這個 repo 由論文工作台主程式自動產生，不要手改 SKILL.md（改了下次會被蓋掉）。授權：MIT。
