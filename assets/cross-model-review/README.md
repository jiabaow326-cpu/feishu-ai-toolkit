# Cross-Model Review 附件

這裡保留飛書工具頁明確提供的兩種來源。檔案只下載、讀取及複製，沒有執行或安裝。

- `codex-review-gate.py` 與 `codex-peer-review.zip`：從原作者公開下載網址保存的原始 bytes。
- `downloaded/codex-peer-review/SKILL.md`：從原下載 ZIP 精確擷取，方便直接閱讀及使用。
- `inline/`：從飛書工具頁的內嵌程式碼精確抽出，方便與下載版本比較。
- `sources.json`：每檔來源 URL、SHA256、大小、ZIP 文件清單，以及兩來源是否相同。

兩來源可能有版本或格式差異，所以各自保留。ZIP 只含 `codex-peer-review/SKILL.md`，未附 LICENSE 檔案。

使用前先閱讀 [完整安裝與驗收說明](../../toolkits/cross-model-review.md)。需要 Claude Code、已登入的 Codex CLI 與 Python 3；選擇全域或專案安裝並對齊監控路徑。原安裝 Prompt 會調整全域 Codex 設定，先依原文確認影響，再執行安裝與四項驗收。