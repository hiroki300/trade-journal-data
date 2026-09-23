# trade-journal-data

このリポジトリは [stock-checker](https://github.com/hiroki300/stock-checker) の
GitHub Actions が自動生成する JSON の公開先です。PWA
[trade-journal](https://github.com/hiroki300/trade-journal) が fetch します。

**⚠️ 手動でファイルを編集しないでください。** 発行元が次回実行時に上書きします。
この README も `stock-checker/publish_data.py` が生成しています。

## stock-checker の GitHub Actions が publish

| ファイル | 内容 |
|---|---|
| `macro_state.json` | 現在のマクロレジーム (normal / caution / storm / halt) と日経の指標 |
| `limit_watchlist.json` | 指値ウォッチリストと到達判定 (平日 17:45 に再判定) |
| `kuribou_candidates.json` | 井村流スクリーナーの候補 (PEG / ROE / 成長 / 売買代金) |
| `candidate_brief.json` | 上記候補の数字を平易な言葉に翻訳したもの (生成AI 不使用) |
| `forward_results.json` | forward 紙トレの採点結果 (計測のみ・選定には還流しない) |
| `forward_human_compare.json` | 人間の売買記録と機械 baseline の比較 (検証 B3) |
| `pullback_candidates.json` | 押し目×決算レーンの候補 (買いシグナルではない) |
| `pullback_charts.json` | 押し目候補の描画用 日足系列 (PWA がチャートを開いたときだけ取得) |
| `event_radar.json` | 当日引け後の開示イベントと値幅の事実 (候補ではなく観測リスト) |
| `yutai_radar.json` | 登録済み優待銘柄の権利付最終日 (事実のみ) |
| `macro_history.json` | レジーム遷移の履歴 (macro_state.json 更新時に append) |

ジョブごとに生成されたファイルだけが更新されます (ソースに無いものはスキップ)。

## trade-journal (PWA) が直接 publish

| ファイル | 内容 |
|---|---|
| `human_paper_trades.json` | 売買記録 (保有・約定)。**実際の売買記録が含まれます** |

⚠️ こちらは**ワークフローではなく PWA が上書きします**。更新されるのはユーザーが
スクリーンショットを取り込んだときだけなので、売買が無い日に更新されないのは正常です。

## 公開ポリシー

⚠️ `human_paper_trades.json` には**実際の売買記録** (銘柄・日付・価格・株数・信用区分)
が含まれます。このリポジトリは public なので、**非公開リポジトリへの移行を予定**
しています。それまでは取り扱いに注意してください。

- 株価データの出典は J-Quants (個人 Standard 会員)
- 配信を止めるには stock-checker の GitHub **Variables** で該当フラグを `0` にします
  (例: `PULLBACK_SCREEN_ENABLED` / `EVENT_RADAR_ENABLED` / `YUTAI_RADAR_ENABLED`)。
  ワークフローは `.github/workflows/daily_run.yml` の 1 本で、`morning_prices` などは
  その中の**ジョブ名**です

## 取得方法

`https://raw.githubusercontent.com/hiroki300/trade-journal-data/main/<filename>`
から取得できます (CORS 許可済み・認証不要)。
