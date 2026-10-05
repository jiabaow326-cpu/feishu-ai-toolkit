# Codex Security Bridge Kit

用兩個 Prompt 判讀 Security Finding 的證據，並把 repository 掃描與 staging、production、第三方及維運驗證串成有明確範圍的清單。

分類：安全、權限與 API 金鑰

## 工具原文

[開啟完整原文](../toolkits/codex-security-bridge.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/feishu-ai-toolkit/main/toolkits/codex-security-bridge.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

要判斷一則安全 Finding 是否成立，或準備上線、重要修復後，需要補齊掃描以外的驗證證據時。

## 前置需求

- Codex 或可讀取授權 repository 的 coding agent；網頁 AI 亦可手動使用，需貼上 Finding、Coverage、相關程式片段或非敏感設定證據。

## 使用方法

1. 有掃描報告時，一次挑一則重要 Finding，複製 Prompt 1，提供完整 Finding、Coverage 與 repository 狀態。
2. 補上可取得的產品安全規則與非敏感證據，核對攻擊路徑、反證、Severity、Confidence 及 Proof Gap。
3. 把判讀報告交給 Prompt 2；也可在準備上線時直接使用 Prompt 2。
4. 依層提供部署與安全控制情況，確認 scope、負責人及期限，保存 P0／P1／P2 證據清單。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| Finding Evidence Explainer | Prompt | 把單一 Finding 拆成攻擊路徑、證據與反證、Severity、Confidence、Coverage 和 Proof Gap，給出證據 verdict。 | [工具檔案](../toolkits/codex-security-bridge.md) |
| Production Blind-Spot Mapper | Prompt | 分開 repository、staging、production、第三方與維運證據，建立含優先級、pass condition、evidence、owner 與期限的安全驗證地圖。 | [工具檔案](../toolkits/codex-security-bridge.md) |

### Finding Evidence Explainer

Finding 難以理解、團隊有爭議，或修復前需要確認範圍與證據時。

1. 貼上 Prompt 1 及一則完整 Finding。
2. 提供 repository／commit／掃描範圍，必要時附 SECURITY.md 或 define-security-policy 輸出。
3. 補充影響 verdict 的非敏感外部事實，確認允許的驗證環境。
4. 檢查 Finding Evidence Review，修正背景事實後保存完整版本。

### Production Blind-Spot Mapper

上線前、重大改版、修復重要 Finding 或 No findings 仍需補齊正式環境證據時。

1. 貼上 Prompt 2 及已有安全文件、Coverage、Finding Review。
2. 依序提供部署系統、repository 證據、staging 能力與 production 控制的非敏感證據。
3. 確認各未知項目的負責人、期限及審查範圍。
4. 保存完整證據地圖，依 P0、P1、P2 順序收集證據；需另外授權才執行會改動環境的操作。

## 使用重點

這組 Prompt 原文要求只讀審查與規劃，不會直接修 code 或操作 production；unknown 不等於通過，READY FOR REVIEWED SCOPE 僅涵蓋列明的範圍。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/ILxywRaMNiiroqk98JgcPxYqnke)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/NRpewfp9MijegCkmNRzcwLWvnDb)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
