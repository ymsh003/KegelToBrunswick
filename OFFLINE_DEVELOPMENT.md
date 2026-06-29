# Kegel to Brunswick Converter: Development Guidelines

## Goal

Kegelのメンテナンス表を、BrunswickのPattern Design形式へローカル環境だけで変換する。
現在の開発段階では、OCR精度改善を優先し、PDF.js/Tesseract.jsなどのCDN利用を許可する。

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

## Runtime Compatibility

- PDF.js/Tesseract.jsなどのCDNライブラリ利用を許可する。
- OCR言語データの外部取得を許可する。
- PDF/XLSXをアプリケーションサーバーへ送信しない設計を維持する。
- 外部フォント、装飾用外部画像は使わない。
- PDF自動読取が最終仕様。現在は内蔵テキスト抽出とPDF.js/Tesseract.jsによるOCR抽出を併用する。
- 表が画像化されているKegel PDFは、埋め込みJPEG画像を抽出してプレビュー表示する。
- 画像内のForward/Reverse表候補を切り出す。
- Forward/Reverse表の各行画像を切り出し、編集可能な入力行へ対応付ける。
- 切り出した行画像に軽量OCRをかけ、候補値として入力欄へ反映する。
- OCR候補は信頼度で色分けする。
- Kegel Rowsへ反映する前に、板目形式と数値形式を検証する。
- OCR結果は必ず目視確認・補正してからKegel Rowsへ反映する。
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
3. Kegel PDF画像からForward/Reverse行画像をより高精度にOCRする。
4. 変換モデルのパラメータをプリセット化。
5. Brunswick機種ごとのテンプレート差分を吸収するセルマッピング定義を追加。
