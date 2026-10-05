# 理解防護套件

用自我訪談檢查是否理解自己的作品，再把說明升級成可分享的單檔 HTML 工作頁。

分類：輸出風格、HTML 與瀏覽器任務

## 工具原文

[開啟完整原文](../toolkits/html-workpage.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/html-workpage.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

已完成 AI 輔助 App、agent、工作流、原型或儀表板，準備放進作品集或 README；或已有 Markdown 說明想提高理解與瀏覽效率。

## 前置需求

- 支援多輪對話的 Claude、ChatGPT 或 Gemini。HTML 生成需要完整原始 artifact 與可輸出完整程式碼的模型；來源建議 Claude 或 Claude Code。

## 使用方法

1. 先使用理解自我訪談，逐一回答『做了什麼、為什麼這樣做、何時會壞、學到了什麼』，生成 Markdown 說明。將說明交給第二組 Prompt，生成單檔 HTML 工作頁。已有說明可直接用第二組。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| 理解自我访谈 | Prompt | 以一題一題的技術訪談追問作品的用途、選擇、失敗情境與學習，產出四段可附在 README 或作品旁的 Explanation Artifact。 | [工具檔案](../toolkits/html-workpage.md) |
| 理解→HTML工作页 | Prompt | 將 Markdown 說明變成可分享、可快速瀏覽的單檔 HTML，包含視覺依賴圖及影響範圍標示。 | [工具檔案](../toolkits/html-workpage.md) |

## 使用重點

應以真實專案與使用者回答為依據；生成 HTML 後仍需自行開啟並驗證內容、連結與圖示。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/IZiswT4f1ieS4vkkxezcXy38nOb)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/TzLSwfafwi7QzrkDiDLcIHhlndf)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
