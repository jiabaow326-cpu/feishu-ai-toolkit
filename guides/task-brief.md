# 任務交辦 Prompt Set：判斷階段、從零建立 Brief、送出前體檢

先判斷任務階段，再建立目標、背景、素材、邊界與完成定義五欄位 Brief，或檢查已有交辦訊息。

分類：任務定義與品質評估

## 工具原文

[開啟完整原文](../toolkits/task-brief.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/task-brief.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

不知道該叫 AI 做什麼，想從模糊想法建立任務，或送出 Prompt 前檢查缺口。

## 前置需求

- Claude、ChatGPT、Gemini 等對話介面；按照引導逐題回答，不必預先整理成完整 Prompt。

## 使用方法

1. 方向不確定時先使用 Stage Decider。進入執行階段後用 Brief Builder 問答建 Brief，將輸出貼到新對話。已經寫好交辦訊息則使用 Brief Auditor 體檢與改寫。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Stage Decider | Prompt | 判定任務處在思考、探索、決定或執行階段，給出適合的指令模式、起手指令與升級到下一階段的條件。 | [工具檔案](../toolkits/task-brief.md) |
| Brief Builder | Prompt | 以逐欄對話收集五欄位資訊，組裝成自然語言完整 Brief 與逐欄速查。 | [工具檔案](../toolkits/task-brief.md) |
| Brief Auditor | Prompt | 逐欄檢查已寫好的 Prompt，指出模糊字眼與缺口，追問後保留原語氣改寫並展示 Before / After。 | [工具檔案](../toolkits/task-brief.md) |

## 使用重點

Prompt 用於定義與審核任務，不等於已完成任務本身。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/XXemwWxxoiA8YTkn0vwc8fctnkf)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/DpnJwF7cCiBHZYk0GRJc8m6VnWd)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
