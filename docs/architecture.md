# Architecture

This umbrella repo documents a 3-part seed pipeline:
LabelGen → Parallel-Scanning → SeedSizer.

## LabelGen (Part 1: Labels + QR)
Input: a .csv or .xlsx file formatted with:
- Row 0 = column flags: "H", "Q", or "H/Q"
- Row 1 = column names
- Row 2+ = data rows. :contentReference[oaicite:0]{index=0}

Processing:
- Reads the sheet, drops blank columns, validates flags, and enforces ≤5 human-visible fields. :contentReference[oaicite:1]{index=1} :contentReference[oaicite:2]{index=2}
- Splits columns into human text vs QR payload (H/HQ vs Q/HQ). :contentReference[oaicite:3]{index=3}
- For each row: builds up to 5 text lines and creates a braced QR string like {Col_Value}{Col_Value}… :contentReference[oaicite:4]{index=4}
- Generates temporary QR PNGs and pastes them into an Avery 5160 PDF layout (3x10 labels/page). :contentReference[oaicite:5]{index=5}

Output:
- A print-ready PDF named AveryLabels.pdf; temporary QR images are deleted after PDF creation. :contentReference[oaicite:6]{index=6} :contentReference[oaicite:7]{index=7}
