# Pipeline Constraints and Conventions

This document defines assumptions that must hold for the pipeline to function correctly.

## LabelGen
- Input tables must place column flags in row 0 and column names in row 1.
- No more than 5 columns may be flagged for human-readable label text.
- QR payload strings are assumed to be unique per seed packet.


## Parallel-Scanning
- Host system must support KVM/QEMU and USB passthrough.
- Each scanner must be exclusively attached to a single VM.
- Scanner QR codes and packet QR codes must be scanned in the correct order.
- Output images are assumed to be 1200 DPI color TIFFs.


## SeedSizer
- Input images must show seeds on a dark, uniform background.
- Image resolution is assumed to be consistent across a batch.
- Each image is assumed to correspond to a single seed packet.


## Cross-Stage Conventions
- QR strings are used as the canonical identifier across all stages.
- Filenames derived from QR strings must remain unchanged between stages.
