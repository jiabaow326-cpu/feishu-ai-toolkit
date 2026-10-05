# Cross-Model Review Kit

提供 Claude Code 一鍵安裝與驗收 Prompt、Stop hook 和 codex-peer-review Skill，讓 plan／spec 在定稿前與 Codex 互審。

分類：程式開發、審查與 Hooks

## 工具原文

[開啟完整原文](../toolkits/cross-model-review.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/cross-model-review.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

已有 Claude Code 和 Codex CLI，希望計畫與規格經獨立模型檢查再交付時。

## 前置需求

- Claude Code、已登入且支援 exec／--json／resume 的 Codex CLI、本機 Python 3。
- 需要確認全域或專案安裝範圍與監控 plan／spec 路徑。
- 原安裝 Prompt 會調整全域 ~/.codex/config.toml；依原文確認影響後再執行。

## 使用方法

1. 複製一鍵安裝 Prompt 給 Claude Code，先做 Codex CLI smoke test。
2. 確認 superpowers 是否使用、全域或專案安裝及 plan／spec 路徑。
3. 安裝後貼上驗收 Prompt，檢查註冊、語法、擋未審文件、放已審文件四項。
4. 手動安裝可使用作者下載的 Python 與 ZIP；飛書內嵌版本另存 inline，兩來源均保留。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| 一鍵安裝 Prompt | Prompt | 建置 Stop hook、合併 settings.json 並放置／對齊 review Skill。 | [工具檔案](../toolkits/cross-model-review.md) |
| Stop hook: codex-review-gate.py | Python Hook | 檢查近期 Write／Edit 的監控路徑，沒有 review marker 時要求互審。 | [工具檔案](../assets/cross-model-review/codex-review-gate.py) |
| codex-peer-review Skill | Skill | 與同一個 Codex session 逐輪修正或反駁，直到取得共識。 | [工具檔案](../assets/cross-model-review/downloaded/codex-peer-review/SKILL.md) |
| 驗收 Prompt | Prompt | 用合成 Stop 事件驗證四項行為，無須呼叫 Codex。 | [工具檔案](../toolkits/cross-model-review.md) |

## 附件與其他原文

- [assets/cross-model-review/codex-review-gate.py](../assets/cross-model-review/codex-review-gate.py)
- [assets/cross-model-review/codex-peer-review.zip](../assets/cross-model-review/codex-peer-review.zip)
- [assets/cross-model-review/downloaded/codex-peer-review/SKILL.md](../assets/cross-model-review/downloaded/codex-peer-review/SKILL.md)
- [assets/cross-model-review/inline/codex-review-gate.py](../assets/cross-model-review/inline/codex-review-gate.py)
- [assets/cross-model-review/inline/codex-peer-review/SKILL.md](../assets/cross-model-review/inline/codex-peer-review/SKILL.md)
- [assets/cross-model-review/sources.json](../assets/cross-model-review/sources.json)

## 使用重點

ZIP 僅含 codex-peer-review/SKILL.md，未附 LICENSE 檔案。

下載檔與飛書內嵌來源均獨立保留；SHA256 差異代表來源版本或格式不同，沒有以其中一版覆蓋另一版。

所有檔案只下載、讀取及複製，未執行或安裝。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/MEQLwF6Nqi97OWkFD3CcrTOQnZe)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/AvlYwcbAHi0rAHkEKivc2kcOnQy)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
