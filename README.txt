HUNTCRAFT — OFFLINE SIEM WORKSPACE

1. Extract the ZIP (Windows: right-click > Extract All).
2. Keep all extracted files in the same folder.
3. Double-click index.html to open it in your browser.
4. Choose Splunk, CrowdStrike, Microsoft Sentinel, or IBM QRadar.
5. Build your query, then copy or export it and run it in your SIEM.

No installation, local web server, login, or internet connection is needed
for query building. No external fonts, scripts, images, or libraries load.
Documentation links and your actual SIEM console require internet or network access.

Use the "Choose platform" link to return to the start page.
CrowdStrike is for CQL in Advanced Event Search / LogScale, not API FQL.
Set the time picker in Falcon separately. Confirm field mappings for your logs.

Saved searches use browser storage. File-based storage behavior varies by
browser and moving this folder may change its storage location. Export
important queries as .spl or .cql files to keep an independent copy.
If copying is blocked, the query is selected; press Ctrl+C (Command+C on Mac).

All actual result rows are produced by your SIEM. The workspace does not
connect to a SIEM or ingest events. Table previews show expected columns.

MICROSOFT SENTINEL
The Sentinel builder produces KQL with TimeGenerated filters and uses project
for table columns. Choose a connected table and verify its field mappings.
Failed-login and PowerShell templates use SecurityEvent; process command
lines require the appropriate Windows audit configuration. The network
template uses CommonSecurityLog (CEF). Custom times are entered in UTC.
Unique counts use dcount() estimates; empty mapped values are excluded.
The console time picker must cover the KQL time range.

IBM QRADAR
The QRadar builder produces AQL for events (Log Activity) or flows (Network
Activity). Time is selected with a trailing LAST clause. Source/destination
IP mappings default to sourceip/destinationip. Hostnames may need custom
properties; enter their exact names in the mappings when available.
COUNT(*) counts Ariel records; SUM(eventcount) is needed for original event
totals in coalesced event data. Payload templates use UTF8(payload) and ILIKE.
This builder supports relative time windows; advanced START/STOP clauses
can be added manually. Apostrophes and line breaks in string input are
rejected by the visual builder; advanced literals need manual query edits.
Queries have been checked for generation, not executed against a live QRadar.

IOC SEARCH
All four builders include bulk IP, URL and SHA-256 filters. Enable IOC search,
map populated types to real log fields, and select OR (any type) or AND
(all populated types in one record). URLs are one per line. Hashes require
64 hexadecimal characters. Optional refanging supports hxxp/hxxps/[.]/[:].
Use IOC filters only clears condition/endpoint filters, preserving scope.
IOC filters are added to the current source/time scope. The tool never
visits indicators. See README.md for matching and schema limitations.
