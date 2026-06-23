# Release Guide

This project distributes IMS TinyTask through GitHub Releases. The formatter download button depends on a stable asset filename:

```text
IMS_tinytask.exe
```

Do not include version numbers in the uploaded executable asset name. Put the version in the Git tag and release title instead.

## Build IMS TinyTask

From a clean checkout on Windows:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
pyinstaller IMS_tinytaskv4\IMS_tinytask.spec --clean --noconfirm
```

The expected executable is:

```text
dist\IMS_tinytask.exe
```

Before uploading, run a quick smoke test:

```powershell
python -m py_compile IMS_tinytaskv4\IMS_tinytask.py
```

Then open `dist\IMS_tinytask.exe`, confirm the IMS TinyTask window starts, and confirm the formatter can connect to `http://127.0.0.1:8765`.

## Create a GitHub Release

1. Go to `https://github.com/arnjrmlim/ims-format/releases/new`.
2. Create a new tag such as `v1.0.0`.
3. Use a release title such as `IMS Format v1.0.0`.
4. Upload `dist\IMS_tinytask.exe` as a release asset.
5. Confirm the uploaded asset is named exactly `IMS_tinytask.exe`.
6. Publish the release.

The formatter uses this direct download URL:

```text
https://github.com/arnjrmlim/ims-format/releases/latest/download/IMS_tinytask.exe
```

After publishing, test the URL in a fresh browser session. It should download the executable immediately. If it opens a GitHub error page, the latest release is missing the asset or the asset filename does not match.

## Updating IMS TinyTask

For each new version:

1. Build a fresh executable from the release commit.
2. Smoke test the executable locally.
3. Create a new Git tag and GitHub Release.
4. Upload the new executable as `IMS_tinytask.exe`.
5. Publish the release.
6. Verify the latest-release download URL still downloads the new executable.

No formatter code change is required when the asset filename remains `IMS_tinytask.exe`.

## Troubleshooting

- **Button opens the GitHub release page:** the repository has no published latest release, or the latest release does not have an asset named `IMS_tinytask.exe`.
- **Old executable downloads:** confirm the intended release is the latest non-draft, non-prerelease release.
- **Browser blocks the file:** confirm users trust the release source and consider code signing future Windows builds.
- **Formatter cannot connect after install:** start IMS TinyTask once so it can register the `ims-tinytask` protocol and local bridge.
