# SCImago Journal Rank snapshots

This directory stores the yearly SCImago Journal Rank (SJR) tables for 2010–2025 and the 2025 SCImago Journal
Value table. They are byte-for-byte copies of a research mirror of the public SCImago downloads, used for journal
and source matching, quartile lookup and estimated article processing charges. The files contain source-level
metadata only.

## Files

| File | Contents |
| --- | --- |
| `scimagojr-2010.csv` to `scimagojr-2025.csv` | One SJR table per year: rank, `Sourceid`, title, type, ISSN, publisher, open-access flags, SJR, best quartile, H-index, document and citation counts, country, coverage, subject categories and areas |
| `scimago-journal-value-2025.csv` | 2025 table with SJR, best quartile, number of documents, an estimated article processing charge and an estimated value, both in USD |
| `SHA256SUMS.txt` | SHA-256 of the 17 data files |
| `manifest.json` | Description of the mirror: years, file pattern, delimiter, encoding, matching keys and checksum policy |
| `repository_state.json` | Verification record of this copy: 17 of 17 files matched `SHA256SUMS.txt` |

## Format

- Semicolon-delimited, UTF-8 without BOM, LF line endings; SJR values use a decimal comma (for example `104,065`).
- `Sourceid` is the SCImago source identifier. ISSNs are written without hyphens; a source with two ISSNs lists
  both, separated by a comma.
- In `scimago-journal-value-2025.csv`, the header names `Publisher` before `Open Access` and `Open Access Diamond`,
  but the data rows give the two open-access flags first and the publisher third, and end with an empty field.
  Read this file by position, or rename the three columns before reading it by header.
- The H-index column repeats the current value in every yearly file, so it is not a historical H-index.
- The APC and value columns are estimates, not publisher prices.

## Source

- SCImago Journal & Country Rank (SCImago Lab; data source: Scopus): https://www.scimagojr.com/
- Research mirror used for this snapshot (mirror update of 2026-10-25, see `manifest.json`):
  https://scopus.cuatui.cloud/du-lieu/scimago/

The files are stored unchanged, and `.gitattributes` marks this directory `-text` so that Git keeps the bytes on
every platform. `SHA256SUMS.txt`, `manifest.json` and `repository_state.json` use Windows line endings. To check
a clone:

```bash
cd SCIMAGO
tr -d '\r' < SHA256SUMS.txt | sha256sum -c -
```

Conference coverage in SCImago varies from year to year. A source missing from one year is not evidence that
Scopus discontinued it, and a source missing from SCImago is not evidence that it is predatory.
