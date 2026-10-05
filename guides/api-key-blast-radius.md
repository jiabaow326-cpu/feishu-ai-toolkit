# API Key 止血包

依專案與外部服務盤點 API keys 及其他憑證的 metadata，檢查最小權限、花費上限、替身 key 與最壞損失，排出優先修整項目。

分類：安全、權限與 API 金鑰

## 工具原文

[開啟完整原文](../toolkits/api-key-blast-radius.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/api-key-blast-radius.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

部署新服務前、定期輪替時，或平台事故後想盤點每把憑證的影響範圍時。

## 前置需求

- Claude、ChatGPT、Gemini 等網頁 AI 即可；準備專案、部署平台、外部服務及憑證用途資訊，不需提供任何 key 或密碼的值。

## 使用方法

1. 開新對話，複製完整 Key Inventory Prompt。
2. 描述專案、部署平台與外部服務，核對 AI 草擬的憑證清單。
3. 逐專案提供環境共用、權限、花費上限、自動儲值與保存位置的 metadata；不確定的項目保留為待確認。
4. 確認背景摘要，檢查盤點表、前三項修整與洩漏後前十分鐘計畫。
5. 重新核對目前官方帳單與權限設定；將不含秘密值的表格保存為 keys.md。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| 爆炸半徑盤點（Key Inventory） | Prompt | 逐憑證盤點權限、額度與撤銷入口，估計最壞損失，列出優先修整與事件初期動作。 | [工具檔案](../toolkits/api-key-blast-radius.md) |

### 爆炸半徑盤點（Key Inventory）

希望把專案憑證的外洩影響範圍、輪替與處理順序整理成可查閱表格時。

1. 貼上完整 Prompt，描述全部專案及外部服務。
2. 補正憑證清單，只提供名稱、供應商、用途、環境與控制設定。
3. 核對每項風險與設定入口，採用修整順序；自行保存 metadata 表格。

## 使用重點

原文內嵌的平台參考標示查證日期為 2026-08-30；本次完整保存作者原文，未重新驗證其即時帳單功能或 UI 路徑。使用前需核對目前官方設定。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/JyZlwlypNicQPkkteFpcmLzknGf)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/AoZFwcvERiQzCPkmcpacCSe3nAA)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
