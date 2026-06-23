# IMS Format

## Overview

IMS Format is an internal productivity tool for converting center or head office Excel workbooks into a normalized main encoding format. The repository includes a browser-based formatter and a Windows macro helper for recording and replaying repetitive input actions.

## Features

- Upload `.xlsx` workbooks in the browser.
- Detect supported center and head office worksheet layouts.
- Normalize payor, insured, member, dependent, contact, privilege, sex, civil status, and date fields.
- Split and clean full names, suffixes, compound surnames, and name components.
- Validate name fields for unsupported special characters before export.
- Preview converted rows with pagination.
- Export a workbook with a new `Formatted` worksheet while preserving source sheets.
- Integrate with a local Windows macro helper through `ims-tinytask://open` and `http://127.0.0.1:8765`.
- Record, save, load, and replay Windows input macros with configurable hotkeys.

## Requirements

- Windows for the Python macro helper.
- Python 3.11 or newer recommended.
- A modern browser for `Formatter.html`.
- Internet access when using the CDN-hosted browser libraries in `Formatter.html`.

Python runtime dependency:

```powershell
pip install -r requirements.txt
```

Browser libraries loaded by `Formatter.html`:

- ExcelJS
- FileSaver.js

## Installation

Clone the repository and install Python dependencies:

```powershell
git clone https://github.com/arnjrmlim/ims-format.git
cd ims-format
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

## Usage

Open `Formatter.html` in a browser, select an `.xlsx` workbook, review the preview and validation messages, then download the converted file.

To run the macro helper from source:

```powershell
python IMS_tinytaskv4\IMS_tinytask.py
```

Executable builds should be published as GitHub Release artifacts rather than committed to the repository.

## Folder Structure

```text
.
├── Formatter.html
├── IMS_tinytaskv4/
│   ├── IMS_tinytask.py
│   ├── IMS_tinytask.spec
│   ├── icon.ico
│   ├── final_tiny.rec
│   └── requirements.txt
├── AUDIT_REPORT.md
├── CONTRIBUTING.md
├── GITHUB_READY.md
├── SECURITY.md
├── requirements.txt
├── .env.example
└── .gitignore
```

Recommended future structure:

```text
.
├── src/
├── assets/
├── docs/
├── tests/
├── output/
├── README.md
├── SECURITY.md
├── CONTRIBUTING.md
├── LICENSE
├── .gitignore
├── .env.example
└── requirements.txt
```

## Configuration

No required environment variables are currently used. The macro helper stores user settings in `%APPDATA%\IMS TinyTask\settings.json`.

Default local integration values:

- Host: `127.0.0.1`
- Port: `8765`
- Protocol: `ims-tinytask`

## Security Notes

- Do not commit `.env`, logs, generated outputs, executable builds, temporary files, or local macro recordings.
- Review workbook data before sharing exported files because encoding workbooks may contain personal or company-sensitive information.
- The macro helper is Windows-only and controls mouse/keyboard input, so run it only from trusted source code.
- Keep executable builds in GitHub Releases or another controlled distribution channel.

## License

No license has been selected yet. MIT is simpler and permissive; Apache 2.0 is also permissive and includes an explicit patent grant. Choose one before publishing publicly.
