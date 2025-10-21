# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Repository overview
- Purpose: a single-page, static HTML resume (`final_resume.html`) with inline CSS and a tiny JS snippet that adds a “Download as PDF” button and guides the user to print-to-PDF with clean margins and no headers/footers.
- No build system, package manager, linter, or tests are configured.

## Common commands
- Open the resume in a browser:

```bash path=null start=null
# macOS
open ./final_resume.html
# Linux
xdg-open ./final_resume.html
```

```powershell path=null start=null
# Windows (PowerShell)
Start-Process .\final_resume.html
# or
explorer .\final_resume.html
```

- (Optional) Serve via a simple local web server if you prefer http:// URLs:

```bash path=null start=null
python -m http.server 8000
# then open http://localhost:8000/final_resume.html
```

Notes:
- There is no lint/test tooling to run. If you add any in the future (e.g., HTML/CSS linters), document the commands here.

## High-level structure and architecture
- Single entry point: `final_resume.html`.
  - Head: inline `<style>` defining layout, typography, colors, and a `@media print` ruleset that adjusts font sizes, hides the print button, and ensures accurate print colors.
  - Body: logically grouped sections with minimal classes, roughly:
    - Header: name/title/contact info.
    - Sections: Professional Summary, Technical Skills (CSS grid layout), Professional Experience (items with headings, durations, bullet achievements), Education, Awards & Achievements, Certifications.
  - Script: on `window.onload`, dynamically creates a styled “Download as PDF” button (`.print-btn`). Clicking shows per-browser instructions and then calls `window.print()`. The `.print-btn` is hidden under `@media print`.
- No external assets or dependencies; everything is inline, so edits are immediate and previewable by reloading the file.

## Editing guidance (code-aware)
- Keep `@media print` rules aligned with on-screen styles; the print button relies on the `.print-btn { display: none !important; }` rule to stay out of the PDF.
- The layout uses simple flex/grid patterns; if adding new sections, reuse existing classes (`section`, `section-title`, grid in `skills-container`) to maintain visual consistency.
