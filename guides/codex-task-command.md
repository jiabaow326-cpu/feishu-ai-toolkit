# Codex 任務指揮工具包

用四支 Prompt 完成交辦前判斷、整理工作資料夾、寫成可驗收任務與驗證成果。

分類：任務定義與品質評估

## 工具原文

[開啟完整原文](../toolkits/codex-task-command.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/codex-task-command.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

剛開始用 Codex，或交辦任務常跑偏、產出難以驗收時。

## 前置需求

- Prompt 1、3、4 可用 Codex、Claude、ChatGPT 或 Gemini。
- Prompt 2 需要 Codex 或 Claude Code 等能讀寫本機檔案的 Agent。

## 使用方法

1. 完整流程按 Prompt 1 → 2 → 3 → 4 執行；亦可只選當前痛點。
2. 複製每一支完整程式碼區塊，貼給適用的 AI。
3. 依它的提問提供任務、來源、範圍和驗收證據；Run Spec 可先單獨試用。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Steer or Dispatch | Prompt | 判斷任務應貼身協作或放手交辦，交付建議、最大風險與下一步。 | [工具檔案](../toolkits/codex-task-command.md) |
| Project Room | Prompt | 盤點資料夾、複製工作素材，產出重複版本、缺漏衝突清單與 working brief。 | [工具檔案](../toolkits/codex-task-command.md) |
| Run Spec | Prompt | 將模糊任務變成有目標、來源、界限、完成條件、升級規則與證據的交辦規格。 | [工具檔案](../toolkits/codex-task-command.md) |
| Is It Real? | Prompt | 根據實際成果和來源，提出抽查點與接受、退回補證據、進一步驗證的結論。 | [工具檔案](../toolkits/codex-task-command.md) |

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/F4i3wBle1iVxTskDMMicOjbDnAg)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/KUBuw6tjnibv8CknYtIcEXJKn0g)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
