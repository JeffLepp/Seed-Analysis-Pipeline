# Architecture

This umbrella repo documents a 3-part seed pipeline:
LabelGen → Parallel-Scanning → SeedSizer.

## LabelGen (Part 1: Labels + QR)

    **Input:**
    - a .csv or .xlsx file formatted with:
        - Row 0 = column flags: "H", "Q", or "H/Q"
        - Row 1 = column names
        - Row 2+ = data rows. 

    **Startup:**
    - Host runs LabelGen.py and selects the CSV/EXCEL file containing label information via a GUI file dialog.

    **Processing:**
    - Reads the sheet, drops blank columns, validates flags, and enforces ≤5 human-visible fields. 
    - Splits columns into human text vs QR payload (H/HQ vs Q/HQ). 
    - For each row: builds up to 5 text lines and creates a braced QR string like {Col_Value}{Col_Value}.
    - Generates temporary QR PNGs and pastes them into an Avery 5160 PDF layout (3x10 labels/page). 

    **Output:**
    - A print-ready PDF named AveryLabels.pdf; temporary QR images are deleted after PDF creation.

## Parallel-Scanning (Part 2: Image Acquisition)

    **Input:**
    - Input to the batch controllers is a set of label QR strings (scanned), optionally paired with scanner color tags.

    **Startup:**
    - Host runs virt-manager (QEMU/KVM).
    - Each scanner is passed through to exactly one VM (exclusive USB ownership).
    - Each VM runs a small Python script (scan.py) that detects the scanner, resets USB, scans, and writes a TIFF.

    **Processing:**
    - launch.sh starts all 8 scanner VMs, opens a tmux session split into two panes (Batch 1 and Batch 2), and runs the batch controller scripts. 
    - Batch controllers SSH into each VM to trigger scans, then SCP the resulting TIFFs back to the host to store.

    **Outputs:**
    - Output is a date-stamped folder of TIFF images organized by scanner color under ~/SeedScans/YYYY-MM-DD/.

## SeedSizer (Part 3: Image-Based Phenotyping)

    **Input:**
    - A folder containing high-resolution flatbed scan images (.tif or .tiff).
    - Images are expected to show bright seeds on a dark background
      (e.g., seeds scanned on a black surface).

    **Startup:**
    - User runs SeedSizer.py and selects the folder containing TIFF images via a GUI file dialog.
    - Image resolution is assumed to be 1200 DPI (used to convert pixels → millimeters).

    **Processing:**
    - Each TIFF image is loaded and converted to grayscale.
    - Otsu’s thresholding is applied to separate seeds from the background.
    - Small objects are removed to reduce noise.
    - Connected components are labeled to identify individual seed objects.
    - Region properties are computed (area, axis lengths, eccentricity, solidity).
    - Pixel measurements are converted to physical units (mm, mm²).
    - Clumped seeds are estimated by comparing object area to the mean seed area.
    - Per-image summary statistics are computed across all valid seeds.

    **Output:**
    - A CSV file named <input_folder>_data.csv written to the parent directory.
    - Each row corresponds to one scanned image and contains aggregated seed metrics
      (count, size statistics, shape statistics, total area).
