# Aroga Data Pipeline Project Plan
**Final Version – April 2025**

## Phase 1: Data Ingestion and Upload (Completed)
**Technologies Used:** Flask, Azure Blob Storage, BeautifulSoup, Pandas

**Key Features:**
- Drag-and-drop upload interface for .csv and .html files.
- HTML content is parsed and saved as Excel.
- Files are saved under the `cleanedfile/` container in Azure Blob Storage.
- Each upload overwrites the previous one for freshness.

## Phase 2: Azure Data Factory Pipeline Automation (Completed)
**ADF Trigger Configuration:**
- Triggered by new file in `cleanedfile/` container.
- Pipeline receives dynamic parameters: `fileName` and `filePath`.

**Pipeline Logic (`ProcessUploaded`)**
- Uses `If Condition` blocks instead of Switch.
- Routes files to corresponding Copy activities:
  - `csvfile.csv` → `CopyCsvUploads`
  - `metadatafile.csv` → `CopyMetadata`
  - `cleaned_output_combined.xlsx` → `CopyCleanedClaims`
- Pre-copy script truncates target SQL table to prevent duplication.

## Phase 3: Data Storage in Azure SQL Database (Completed)
**Tables:**
- `dbo.CsvBillingUpload`
- `dbo.CsvMetadata`
- `dbo.Records`

**Data Loading Logic:**
- Insert mode with TRUNCATE script.
- Column mappings defined explicitly.

## Phase 4: Power BI Integration (Completed)
**Setup:**
- Connected Azure SQL DB to Power BI Desktop.
- Enabled scheduled refresh for dashboards.

**Dashboards:**
- Billing Overview (CsvBillingUpload)
- Metadata Logs (CsvMetadata)
- Record Summary (Records)

## ✅ Final Summary
- End-to-end automation from upload to SQL ingestion.
- No manual trigger needed — fully event-driven.
- Real-time reporting with Power BI.
- Clean, scalable, and version-controlled (via GitHub).
