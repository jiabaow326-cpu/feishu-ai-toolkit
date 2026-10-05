# Goal & Taste Toolkit

將模糊任務寫成可驗證的長任務目標，並從對 AI 產出的修改歷史提煉品質標準。

分類：任務定義與品質評估

## 工具原文

[開啟完整原文](../toolkits/goal-taste.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/goal-taste.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

Agent 很快停下來、做完後不符合期待，或主觀品質只能說出『差一點』『太 AI 味』時。

## 前置需求

- 支援對話追問的 AI。目標定義需要預期結果、驗證、限制、權限邊界、迭代策略與卡住停止條件；品味提煉需提供三至五次拒絕或修改 AI 產出的具體例子。

## 使用方法

1. 客觀任務直接使用 Goal Definer。寫作、設計或行銷等主觀任務，先用 Taste Distiller 建立 Taste Profile，再放入 Goal Definer 的 Verification 欄位。將生成的 goal prompt 交給支援長任務的 agent。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Goal Definer | Prompt | 用對話追問 outcome、verification、constraints、boundaries、iteration policy、blocked stop condition 六要素，輸出任務診斷、完整 goal prompt 與使用提醒。 | [工具檔案](../toolkits/goal-taste.md) |
| Taste Distiller | Prompt | 從拒絕與改寫案例找出三至六個偏好，建立每項一至五分 rubric，輸出 Markdown 與 JSON 的 Taste Profile 及可重用指令。 | [工具檔案](../toolkits/goal-taste.md) |

## 使用重點

兩組 Prompt 本身用來定義目標與評估標準，不執行任務。/goal 與 evaluator hook 能否使用取決於接收端版本及環境。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/MvcVwkcWwi2Ji6kBv12cKZbxnMc)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/FVdnwzevdiOPfskXsT8cD1Cenmc)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
