# Kegel to Brunswick Pattern Converter Prototype

Kegel形式のオイルパターンPDFを、Brunswick形式のPattern Design Excelへ変換するためのオフライン試作ツールです。

## Current Status

This is a prototype.

- The final goal is PDF-driven conversion from Kegel pattern sheets to Brunswick pattern workbooks.
- The current build can generate a Brunswick workbook by rewriting a local Brunswick template XLSX.
- PDF extraction is not complete yet.
- The Kegel row table in the UI is currently an intermediate/manual correction layer.

## Offline Policy

The app is designed for offline lane-maintenance environments.

- No CDN
- No external API
- No cloud upload
- No external font or image dependency
- Runs as a single local HTML file

## How To Use

1. Open `index.html` in Microsoft Edge or Chrome.
2. Select a Kegel PDF. This is the intended final input path; PDF parsing is still under development.
3. Confirm or edit the Kegel row data.
4. Select a local Brunswick template XLSX.
5. Review the generated 39-board table.
6. Export the converted Brunswick XLSX.

## Important Notes

Do not publish official tournament PDFs, proprietary Brunswick templates, or generated workbooks unless you have permission to redistribute them.

The included files are source/prototype files only. Users should supply their own PDF and XLSX template locally.

## Files

- `index.html`: Offline web prototype
- `OFFLINE_DEVELOPMENT.md`: Development policy and implementation notes

## Next Work

1. Implement reliable Kegel PDF table extraction.
2. Validate generated XLSX files in Excel on real Brunswick templates.
3. Compare multiple official conversion pairs.
4. Add template-specific cell mapping profiles if different Brunswick workbook versions vary.
