# CLAUDE.md／AGENTS.md 健檢 Prompt

逐條核對有效指令載入來源、專案現況與可查證事實，按選擇對照目前模型官方提示指南，建議留、改、搬、刪或待驗。

分類：AI 指令文件與 Skills

## 工具原文

[開啟完整原文](../toolkits/claude-md-checkup.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/claude-md-checkup.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

升級模型、指令檔越寫越大、AI 不聽規則，或接手他人專案時。

## 前置需求

- Claude Code 或 Codex，需要讀取真實專案檔案。
- 純網頁聊天工具無法直接檢查本機專案。

## 使用方法

1. 在要檢查的專案資料夾開啟 Claude Code 或 Codex。
2. 將完整 Prompt 貼入；選擇是否依目前模型的官方 prompting guide 檢查。
3. 檢視逐條建議與證據；此 Prompt 只讀，不會直接改檔。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| The CLAUDE.md Checkup | Prompt | 建立有效指令鏈，逐條給原文、建議、證據與搬移目的地，先驗證後修剪。 | [工具檔案](../toolkits/claude-md-checkup.md) |

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/FAo7w8iUai3TaPkgmZgccpkCnid)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/H9NEw9Ph9ihBshk2D9BcPJHSnEe)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
