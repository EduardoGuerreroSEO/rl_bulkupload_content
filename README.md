# Ralph Lauren Content Asset SEO XML Generator

Adaptation of the category SEO generator for SFCC content assets.

## Use

1. Serve the `dist` directory on your normal web host (or run `python -m http.server 8000 --directory dist`).
2. Use the same login credentials as the original generator.
3. Select EU or ME and the required markets. The original JSON market configuration is unchanged.
4. Download the Excel template. Use three headers: `content_id`, `title`, `desc`.
5. Name workbooks by source language: EN.xlsx, FR.xlsx, DE.xlsx, ES.xlsx, IT.xlsx, NL.xlsx, PT.xlsx, PL.xlsx, SE.xlsx for EU; EN.xlsx or AR.xlsx for ME.
6. Upload workbooks, preview the first asset if needed, and generate the ZIP.
7. In SFCC Content > Import & Export, select the intended site/library and UPDATE mode. Import either the COMBINED XML or the individual language XML files.

The editable Library ID box defaults to RalphLauren_EU_Library. Replace it with an exact different shared-library ID when needed, or clear it to target the selected site's private library. The current field value is used in both previews and downloads.

## Behaviour

- Same regions, markets, locale mappings, country-code substitutions, currency-symbol substitutions, ME brand substitutions, background and login as the original.
- Currency amounts are not converted. Country-code replacements follow the original algorithm and affect matching uppercase codes anywhere in the text.
- Output uses the SFCC library namespace, content-id, page-title and page-description.
- Only the first worksheet is read. Empty title/description cells are omitted and leave the existing field unchanged; at least one field is required per row.
- Multiple files for the same language are merged. Conflicting values for one asset/locale/field block download.
- No selected markets means no output for that language. A file error blocks the entire ZIP rather than generating partial output.
- The combined file groups all locale fields under each content asset once.
- The generator does not connect to or import into SFCC. Metadata is processed in the browser.
- The original JavaScript login is retained for compatibility; use host-level authentication if actual access control is required.
- SheetJS 0.20.3, JSZip and FileSaver load from CDNs, as in the original tool. No vendor folder is required. Tailwind, Prism and fonts retain external CDN loading as in the original.

## Validation

Real Excel-to-ZIP tests passed for EU and Arabic ME, multilingual consolidation, conflicting updates, deselected markets, XML escaping and blank fields. Generated content XML validated against the official Salesforce library.xsd. No SFCC import was performed. Visual browser QA was unavailable in the execution environment.

GitHub Pages: put index.html, markets_eu.json, markets_me.json and background.avif together in the publishing directory. Refresh with Ctrl+Shift+R after updating.
