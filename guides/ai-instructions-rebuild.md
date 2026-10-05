# AI Instructions Rebuild Set

逐條審查一份 CLAUDE.md、AGENTS.md、Custom Instructions 或 Skill，整理 KEEP、REWRITE、MOVE_TO_REFERENCE 與 DELETE_CANDIDATE，產出完整精簡候選版與待測清單。

分類：AI 指令文件與 Skills

## 工具原文

[開啟完整原文](../toolkits/ai-instructions-rebuild.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/ai-instructions-rebuild.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

設定文件持續膨脹、更換模型後要重檢舊規則，或重複規定造成 source of truth 不清楚時。

## 前置需求

- 可閱讀長文字並多輪問答的 AI；一次提供一份完整設定文件。具檔案權限時可提供路徑，否則貼上內容；最好另有用途、載入時機與好壞結果範例。

## 使用方法

1. 先保存原始文件，選擇一份設定文件並移除敏感資訊。
2. 複製完整 Prompt，選擇回覆語言，提供可讀路徑或完整文字。
3. 補充用途、載入時機、實際任務、不能違反的邊界與既有證據；確認 scope summary。
4. 保存逐條決定表、資訊架構、完整候選版、reference 草稿與待測清單。
5. 用相同模型、真實任務及驗收標準比較目前版與候選版，再決定採用哪些改動。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| 精簡 AI 設定文件 | Prompt | 檢查行為效果、資訊來源、載入範圍、重複內容、完成條件及風險，提出可追溯的重寫候選與驗證方法。 | [工具檔案](../toolkits/ai-instructions-rebuild.md) |

### 精簡 AI 設定文件

整理一份給 AI 消費的設定文件，保留必要邊界並將情境專屬資訊移到適當位置時。

1. 貼上完整 Prompt，一次提供一份文件。
2. 回答缺少的背景問題並核對範圍摘要。
3. 檢查所有來源單元的決定表、主文件與 reference 草稿。
4. 保存候選與測試清單；完成比較後由使用者決定是否採用。

## 附件與其他原文

- [toolkits/ai-instructions-rebuild-variant.md](../toolkits/ai-instructions-rebuild-variant.md)

## 使用重點

這個 Prompt 只產出文字，不直接修改或覆寫檔案。DELETE_CANDIDATE 是待測候選，不代表可以安全刪除。另有繁體說明版本，兩份完整原文皆保留。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/YmOawX3evi0cBYkHj6EcGvA3ngf)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/NqfJwhiqTiAGM4kpP60cvMQMnBf)
- [AI Instructions Rebuild Set（繁體說明原文版本）](https://kcn4ucks9zgj.feishu.cn/wiki/XGObweZnli4h86k1szgc5f81noh)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
