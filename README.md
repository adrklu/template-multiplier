# Template Multiplier

A browser-based tool that turns one docxtemplater `.docx` master into numbered template variants using a mapping JSON.

This is built for specific business patterns. Unusable without context beyond 

## What

- Takes a quote 1/master `.docx`
- Takes a separate mapping `.json`
- Generates quote 1, quote 2, and quote 3 downloads
- Keeps quote 1 as a direct clone
- Applies quote-specific field suffixes for quote 2 and quote 3
- Applies explicit component mappings where the target names are not linear
- Rewrites quote condition literals such as `Quote 1` to `Quote 2` / `Quote 3`

## How

Drop in the master `.docx`, drop in the mapping JSON, set an output filename pattern like:

```text
agreement{quote}.docx
```

`{quote}` is blank for quote 1, then becomes `2` and `3`.

Click generate. The page downloads the generated files. Everything runs in the browser.

## Mapping

No mapping is embedded in the page. The mapping stays as a separate JSON file to allow for ambigious GitHub pages hosting.

The mapping defines:

- `quoteSpecificDataFields` - fields that should become `field2` and `field3`
- `jobWideDataFields` - fields that must stay unchanged
- `componentMappings` - explicit non-linear component collection mappings
- `quoteLiteralMappings` - condition text mappings

If a master contains a `model.data.*` field that is not listed as quote-specific or job-wide, the script throws an error.

## Technical

- Uses [PizZip](https://github.com/open-xml-templating/pizzip) to read/write `.docx` archives in the browser
- Processes Word XML files under `word/*.xml`
- Replaces tag text only; it does not restructure Word runs or paragraphs
- Generates files locally; no uploads, no server, no tracking

## Live

[https://adrklu.github.io/template-multiplier/](https://adrklu.github.io/template-multiplier/)
