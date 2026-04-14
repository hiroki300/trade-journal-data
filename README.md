# trade-journal-data

このリポジトリは [stock-checker](https://github.com/hiroki300/stock-checker) の
GitHub Actions が自動生成する JSON データの公開先です。

**⚠️ 手動でファイルを編集しないでください。** 次のワークフロー実行で上書きされます。

## ファイル一覧

| ファイル | 内容 | 更新タイミング |
|---|---|---|
| `macro_state.json` | 現在のマクロレジーム・NY市況等 | daily / weekly |
| `macro_history.json` | レジーム遷移履歴（最新30件、自動 append） | regime 変化時 |
| `weekly_results.json` | 週次分析結果（slim 版） | weekly |
| `limit_watchlist.json` | 指値ウォッチリスト | daily / weekly |
| `journal_analysis.json` | AI 統合分析結果 | daily / weekly |
| `latest_prices.json` | 監視銘柄の前日終値 | 平日 7:30 JST |

## 利用先

- [trade-journal](https://github.com/hiroki300/trade-journal) (PWA, GitHub Pages)
  - `https://raw.githubusercontent.com/hiroki300/trade-journal-data/main/<filename>` から fetch
  - CORS 許可済み・認証不要

## 公開ポリシー

- 個人の保有銘柄・売買履歴は含まれません（trade-journal の IndexedDB ローカルのみ）
- 株価データの出典は J-Quants （個人 Standard 会員）
- 配信を停止したい場合は stock-checker 側の `morning_prices.yml` 等を無効化してください
