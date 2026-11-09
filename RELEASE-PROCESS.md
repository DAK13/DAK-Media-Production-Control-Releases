# DAK Media Production Control — public releases

This repository is for compiled Windows installer releases and update metadata ONLY. Source code, production data, operator PINs, API keys and PowerPoint Companion credentials must never be committed here.

## Release process

1. Build and test the Windows NSIS installer from the private source repository on a Windows build machine.
2. Upload the installer as an asset on a GitHub Release tagged `vX.Y.Z`. Use filename `DAK-Media-Production-Control-Setup-X.Y.Z.exe`.
3. Compute SHA-256 of the **exact uploaded installer** (PowerShell: `Get-FileHash .\DAK-Media-Production-Control-Setup-X.Y.Z.exe -Algorithm SHA256`).
4. After the installer has been published and verified, update `update.json` on the main branch to advertise the release. Do not advertise unbuilt or untested versions.

Example update.json (EXAMPLE ONLY; do not publish until real assets exist):

```json
{
  "version": "2.3.1",
  "url": "https://github.com/DAK13/DAK-Media-Production-Control-Releases/releases/download/v2.3.1/DAK-Media-Production-Control-Setup-2.3.1.exe",
  "sha256": "REPLACE_WITH_ACTUAL_SHA256",
  "notes": "Release notes here",
  "companion": "No update required"
}
```

Production Control checks `https://raw.githubusercontent.com/DAK13/DAK-Media-Production-Control-Releases/main/update.json`. A missing manifest means no update is published yet. The app verifies the installer SHA-256 and checks production activity before launching an installer.

## Important limits

The current updater requires the operator to complete the installer after the application closes. It does not yet automatically restore application binaries after a failed install, nor does it implement code-signature verification. Data backup is separate from binary rollback. Never apply an update during a live production.

The source repository remains private: `DAK13/DAK-Media-Production-Control`.
