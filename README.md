# HuntCraft

**Offline SIEM Query Builder** by [Dreams of Tragedy](https://github.com/DreamsofTragedy).

Build investigation queries for Splunk, CrowdStrike, Microsoft Sentinel, and IBM QRadar from one offline workspace.

## Get started

1. Extract the archive and keep the files together in the `HuntCraft` folder.
2. Open `index.html` in your browser.
3. Choose a platform and configure its data source and field mappings.
4. Add filters and choose the output columns.
5. Copy or export the query, then run it in your SIEM.

No installation, local server, or internet connection is needed for query generation. Your SIEM console and external documentation links require network access.

## Supported platforms

| Platform | Language | Search environment |
| --- | --- | --- |
| Splunk | SPL | Splunk Search |
| CrowdStrike | CQL | Falcon Advanced Event Search / LogScale |
| Microsoft Sentinel | KQL | Sentinel / Log Analytics |
| IBM QRadar | AQL | Ariel events and flows |

CrowdStrike CQL differs from legacy Event Search SPL and Falcon API FQL.

## Features

- Multiple source and destination hosts/IPs, with input deduplication.
- Editable field mappings and AND/OR condition groups.
- Event/record tables, grouped counts, unique endpoint counts, and connection pairs.
- Investigation templates, editable query previews, copy, export, and saved searches.
- Dynamic search-to-table fields in the CrowdStrike, Sentinel, and QRadar builders.
- A local start page and return navigation in each builder.

Saved searches use browser storage; behavior can vary for local files. Export important queries to keep a separate copy. Loading a saved query replaces the preview without reconstructing the builder controls.

## IOC search

Each builder includes an **IOC search** section and navigation shortcut.

1. Enable IOC filters.
2. Paste IP addresses, URLs, and/or SHA-256 hashes.
3. Map each populated IOC type to fields that actually exist in the selected data source.
4. Keep **OR** selected to find records matching any IOC type, or choose **AND** to require every populated type to match one record.
5. Select event/record output and keep **Include populated IOC fields** checked to show those columns.
6. Review, copy, and run the query in your SIEM.

URLs use one indicator per line, so commas inside a URL remain intact. IPs and hashes also accept comma-separated lists. SHA-256 hashes must contain exactly 64 hexadecimal characters. Duplicate indicators are removed after optional refanging (`hxxp`, `hxxps`, `[.]`, `[:]`). Hash matching ignores letter case; URL matching uses the complete value and preserves URL path/query case. IP matching is textual; alternative IPv6 spellings and URL normalization differences may require additional indicators.

IOC filters are ANDed with existing conditions and scope. **Use IOC filters only** clears condition and endpoint filters while retaining scope, time range, and IOC input. The tool never connects to or visits an IOC.

URL and hash fields vary by data source and may need custom extraction. QRadar URL/hash fields may be custom properties. Sentinel network, file, and process indicators may reside in different tables, and CrowdStrike indicators may require different event types. Use separate searches when the selected source does not contain all mapped fields. Empty or missing mappings for populated IOC types block query generation. For Splunk, CrowdStrike and Sentinel this IOC interface accepts simple column identifiers; QRadar also supports property names containing spaces.

IOC query generation and validation were checked for all four languages; live SIEM execution remains unverified.

## Field and time settings

Confirm every table, index, event type, and property against your environment. Templates are starting points and may require different fields or enabled connectors.

- **Splunk:** use the correct index, sourcetype, and field extractions.
- **CrowdStrike:** set the time range in Falcon; verify local/remote direction and event-specific mappings.
- **Sentinel:** KQL includes a time filter; custom inputs use UTC. The console time picker must cover the query window.
- **QRadar:** relative windows use `LAST`. `COUNT(*)` counts Ariel records; coalesced-event totals may need `SUM(eventcount)`.

Unique counts and aggregation limits differ by platform. See `README.txt` and each builder's query notes for details.

## Project files

Upload the contents of the `HuntCraft` folder to your repository root. The five HTML pages use relative links and embedded scripts/styles.

The included JPEG screenshots were supplied with the working archive and show the interface before the HuntCraft rename. New screenshots should be captured from these renamed pages before using them as current branding images.

## Validation

Branding, JavaScript syntax, local navigation, and archive integrity were checked. Queries have not been executed against live SIEM deployments. Browser rendering remains unverified. Input checks do not validate tenant schemas, permissions, or complete query-language syntax.

## Contributing

Include the platform, builder settings, generated query, expected behavior, and a sanitized error message when reporting issues. Remove sensitive information from examples and screenshots.

## License

No license has been selected. Add a `LICENSE` file if you want to grant reuse rights explicitly.
