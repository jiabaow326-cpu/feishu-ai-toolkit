# AI 分工系統建立 Prompt Kit

評估新 AI 工具、審查目前工具組合，並把真實任務分配到合適工具的三組 Prompt。

分類：工具選擇與模型分工

## 工具原文

[開啟完整原文](../toolkits/ai-routing-system.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/ai-routing-system.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

新工具推出時猶豫是否投入時間，付費工具花費與實際工作不匹配，或想建立個人與團隊 AI 分工地圖。

## 前置需求

- 可進行來回對話的 AI；工具評估需提供發布內容、目前工具清單、工作角色與資料位置。原文對新工具評估建議使用推理能力較強的模型。

## 使用方法

1. 可以各自使用。重整工具組合時先跑 AI Stack Audit，將浪費與缺口輸出交給 Personal Routing Map Builder。日後遇到新工具，再用 Tool Launch Filter 判斷是否加入。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Tool Launch Filter | Prompt | 用連接能力、開放性、資料存取、生態系與疊加性五個維度評估新工具，產出評分表、go/no-go 判斷、三個行動與五行分享卡。 | [工具檔案](../toolkits/ai-routing-system.md) |
| AI Stack Audit | Prompt | 將付費 AI 工具對應到實際工作，找出不匹配、浪費與缺口，產出適配矩陣、一頁管理備忘錄及三項優先行動。 | [工具檔案](../toolkits/ai-routing-system.md) |
| Personal Routing Map Builder | Prompt | 依需要什麼資料、資料在哪裡、哪個 AI 能讀寫三問，將常見工作分到預設工具、專門 wrapper 或其他產品，產出分工地圖與切換成本提醒。 | [工具檔案](../toolkits/ai-routing-system.md) |

## 使用重點

工具推薦必須連到使用者的實際任務與資料；原文模型版本為來源建議，尚未另行驗證目前服務可用性。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/H0dRwqhtligC1OkyBkdcBaGDnlf)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/PTWUw3fPGiiMpckC1aLc8gaWnWg)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
