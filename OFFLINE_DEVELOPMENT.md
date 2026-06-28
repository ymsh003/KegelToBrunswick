# Kegel to Brunswick Converter: Offline Development Guidelines

## Goal

Kegelのメンテナンス表を、BrunswickのPattern Design形式へローカル環境だけで変換する。
現場ではインターネット接続がない前提とし、外部API、CDN、クラウド保存を使わない。

## Application Shape

- 単体HTMLを基本配布物にする。
- 変換ロジック、ZIP/XLSX更新処理、UIをHTML内に同梱する。
- Kegel PDFを主入力にする。
- BrunswickテンプレートXLSXは出力先フォーマットとして利用者がローカルファイルから選択する。
- 出力はローカルに保存されるXLSXとCSVに限定する。

## XLSX Rewrite Policy

- テンプレート全体を新規生成しない。
- 既存のBrunswick XLSXを読み込み、`xl/worksheets/sheet1.xml` の必要セルだけを書き換える。
- 書き換え対象はまず以下に限定する。
  - `G21, K21, O21, S21, W21, AA21`: ゾーン終了距離
  - `C29:AO34`: 6ゾーン x 39板目の噴霧率
- グラフ、比率表、隠しシート、数式はテンプレート側の既存構造を維持する。
- `xl/calcChain.xml` は出力時に削除し、`workbook.xml` に全再計算指定を入れる。
- Excelで開いた際にRatio、Lengthwise Ratio、Pattern Graphが再計算されることを前提にする。

## Offline Compatibility

- CDNライブラリを使わない。
- 外部フォント、外部画像、Web API送信を使わない。
- PDF自動読取が最終仕様。現在は外部ライブラリなしのPDFテキスト抽出に対応する。
- 表が画像化されているKegel PDFは、次段階でOCRまたは画像解析が必要。
- Kegel行データ入力欄は、PDF抽出結果の確認・補正用として扱う。
- 対応ブラウザは現実的にMicrosoft EdgeまたはChrome系を想定する。

## Validation Steps

- 変換後の39板目表を画面で確認する。
- CSVとXLSXの値が一致していることを確認する。
- テンプレートExcelを開き、Pattern Designの値とグラフが更新されることを確認する。
- 公式変換済みXLSXがある場合は、RMSEと最大差分でモデルを調整する。

## Next Development Steps

1. XLSX出力をExcelで開く実機検証。
2. 複数パターンで公式変換結果との比較。
3. Kegel PDF画像からForward/Reverse表をOCRまたは画像解析で半自動抽出。
4. 変換モデルのパラメータをプリセット化。
5. Brunswick機種ごとのテンプレート差分を吸収するセルマッピング定義を追加。
