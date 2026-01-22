# Data Flow

This document describes files, folders, naming rules, and hand-offs between pipeline stages.

## Artifacts (what moves through the pipeline)
- Plot table (.csv/.xlsx) → LabelGen
- QR payload string (packet identifier) → Parallel-Scanning
- Scan images (.tif/.tiff) → SeedSizer
- Metrics table (.csv) → downstream analysis

## Stage 1: LabelGen → Outputs
**Consumes:** plot table (.csv/.xlsx)  
**Produces:** AveryLabels.pdf  
**Identifier created:** QR payload string format: {...}{...}

## Stage 2: Parallel-Scanning → Outputs
**Consumes:** packet QR strings (scanned)  
**Produces:** TIFF images
**Output layout:** ~/SeedScans/YYYY-MM-DD/<Color>/*.tiff  
**Filename rule:** <QR string with spaces→underscores>.tiff

## Stage 3: SeedSizer → Outputs
**Consumes:** folder of TIFF images  
**Produces:** <folder>_data.csv (one row per image)

## Cross-Stage Rules
- QR string is the canonical ID. Do not rename derived filenames before SeedSizer.
- Keep scans from a session in a single folder/date to preserve batch integrity.

## Example Mapping (optional)
plot row → QR string → TIFF filename → metrics row
