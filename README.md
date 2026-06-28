# Kegel to Brunswick Pattern Converter Prototype

Kegel形式のオイルパターンPDFを、Brunswick形式のPattern Design Excelへ変換するためのオフライン試作ツールです。

## Current Status

This is a prototype.

- The final goal is PDF-driven conversion from Kegel pattern sheets to Brunswick pattern workbooks.
- The current build can generate a Brunswick workbook by rewriting a local Brunswick template XLSX.
- PDF extraction has a first offline text-parser pass.
- Image-only Kegel PDFs can be detected and previewed by extracting embedded JPEG images.
- Forward/Reverse table rows are cropped into an editable image reader.
- A lightweight offline OCR pass can fill candidate values for fixed-layout row images.
- OCR output must be visually checked before applying it.
- The Kegel row table in the UI is an intermediate/manual correction layer.

## Offline Policy

The app is designed for offline lane-maintenance environments.

- No CDN
- No external API
- No cloud upload
- No external font or image dependency
- Runs as a single local HTML file

## How To Use

1. Open `index.html` in Microsoft Edge or Chrome.
2. Select a Kegel PDF. Text-based Kegel tables are imported into the row editor automatically when possible.
3. If the PDF is image-only, review the extracted page, table candidate crops, and row image reader.
4. Use OCR candidate input or enter the row values manually.
5. Visually check and correct the row values, then apply them to the Kegel row editor.
6. Select a local Brunswick template XLSX.
7. Review the generated 39-board table.
8. Export the converted Brunswick XLSX.

## Important Notes

Do not publish official tournament PDFs, proprietary Brunswick templates, or generated workbooks unless you have permission to redistribute them.

The included files are source/prototype files only. Users should supply their own PDF and XLSX template locally.

## Files

- `index.html`: Offline web prototype
- `OFFLINE_DEVELOPMENT.md`: Development policy and implementation notes

## Next Work

1. Improve OCR accuracy for the extracted Forward/Reverse row images.
2. Validate generated XLSX files in Excel on real Brunswick templates.
3. Compare multiple official conversion pairs.
4. Add template-specific cell mapping profiles if different Brunswick workbook versions vary.
