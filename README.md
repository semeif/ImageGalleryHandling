# ImageGalleryHandling
A small toolbox of PowerShell scripts to clean up large photo/video libraries on Windows. It covers the whole flow: find exact duplicates, detect visually identical images, organize files by capture date, and safely move duplicates out of the way — all with dry-run support, logs, and robust error handling.

## Highlights

Exact duplicates: fast SHA-256 based detection by file size → hash.

Visual duplicates: perceptual hashing (dHash, EXIF orientation aware) to catch pixel-identical images even if metadata or filenames differ. Optional cache + parallelism for big libraries.

Organizer: move photos/videos into Root\YYYY\MM MonthName using EXIF DateTimeOriginal, Windows Shell “Date taken” (DE/EN), or file timestamps as fallback.

Safe moves: retries on locked files, unique destination names, -WhatIf dry runs, and CSV logs.

Case-insensitive extension handling (e.g., .jpg and .JPG both included).

Corrupt files are skipped gracefully (warning instead of abort).

## Included scripts

Organize-ByCaptureDate.ps1 – Sorts into year/month folders.

Find-Duplicates.ps1 – Exact dupes (FastMode) or heuristic scan with optional hashing; writes CSV.

Test-DupeDebug.ps1 – Diagnostics for size groups & hash groups.

Find-VisualDuplicates.ps1 – Perceptual hash pairwise scan (for smaller sets or deep checks).

Export-VisualDuplicateClusters.ps1 – Fast pHash clustering with cache/parallel; marks one “keep” per group.

Move-VisualDuplicates.ps1 – Reads pair CSV, builds clusters, and moves duplicates to a target folder, keeping the shortest filename per cluster.
