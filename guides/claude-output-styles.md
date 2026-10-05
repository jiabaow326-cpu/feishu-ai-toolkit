# 三套 Output Style 一鍵安裝包

三套 Claude Code Output Style 原始文件，以及安裝與專屬風格校準 Prompt。

分類：輸出風格、HTML 與瀏覽器任務

## 工具原文

[開啟完整原文](../toolkits/claude-output-styles.md) · [下載／檢視純文字](https://raw.githubusercontent.com/jiabaow326-cpu/shen-one-san-ai-toolkit/main/toolkits/claude-output-styles.md)

提示詞、程式碼與設定保留來源原文。要複製提示詞時，選取該項完整區塊；若原文含巢狀程式碼區塊，請使用純文字連結，避免漏掉後半段。

## 何時使用

AI 回報的術語、句子密度或結構不符合自己的技術背景，想讓技術小白、PM、vibe coder 或工程師更容易理解輸出時。

## 前置需求

- 已安裝 Claude Code。原始 style 包含 name、description、keep-coding-instructions: true 的 frontmatter。安裝到全域 ~/.claude/output-styles/ 或目前專案 .claude/output-styles/，依原文使用 /output-style 或 /config 切換。

## 使用方法

1. 手動安裝可從 assets/claude-output-styles/ 取得三份 .md，複製到選定的 output-styles 資料夾，再切換風格。也可將原文安裝 Prompt 交給 Claude Code，回答全域或專案、啟用哪套風格兩個問題。客製化時貼一段難讀的 AI 回覆，提供技術背景、討厭的寫法與團隊固定用語，挑選五種改寫並迭代。

## 各項工具與作用

| 工具 | 類型 | 作用 | 完整內容 |
| --- | --- | --- | --- |
| 一键安装 Prompt | Prompt | 下載三套 Output Style、放入指定位置、驗證 frontmatter，並在保留既有設定的前提下啟用使用者選定的風格。 | [工具檔案](../toolkits/claude-output-styles.md) |
| Tech Translator | Output Style | 給無工程背景的使用者。保留真實技術詞、附白話解釋，每次交代做什麼、為什麼、是否成功與下一步。 | [工具檔案](../assets/claude-output-styles/beginner-tech-translator.md) |
| STE100 Brief | Output Style | 給 PM 與有經驗的 vibe coder。以短句、主動語態、固定詞彙和結果優先回報，說明產品影響並標示假設。 | [工具檔案](../assets/claude-output-styles/pm-ste100-brief.md) |
| Engineer TL;DR | Output Style | 給工程師。用簡短同事式回報先說改了什麼、是否可用與意外狀況，省略已知術語解釋。 | [工具檔案](../assets/claude-output-styles/engineer-tldr.md) |
| 风格客制化 Prompt | Prompt | 診斷難讀回覆的問題，產出五種風格供挑選與混合，從實際選擇提煉規則，生成可安裝的專屬 Output Style。 | [工具檔案](../toolkits/claude-output-styles.md) |

## 附件與其他原文

- [assets/claude-output-styles/output-styles-pack.zip](../assets/claude-output-styles/output-styles-pack.zip)

## 使用重點

同名文件覆寫與 settings.local.json 修改依原 Prompt 要先確認、備份並合併；客製化改寫應保留原回覆的每個事實、風險與下一步。

## 來源

- [來源文章](https://kcn4ucks9zgj.feishu.cn/wiki/GA25wAYp5ie39AkwPhacaq7RnfJ)
- [飛書工具頁](https://kcn4ucks9zgj.feishu.cn/wiki/JXIKwzNGQiDFORkMmGDc7KGvn1c)

飛書來源可能需要原帳號的存取權；本倉庫內的工具與附件可以直接閱讀、下載。

[返回分類目錄](../README.md)
