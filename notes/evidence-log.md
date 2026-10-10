# Evidence log

This log records the evidence collected during the analysis. Add screenshots only after checking that they do not expose private information and that the developer has agreed to publication.

| Evidence ID | Evidence | Recorded result | Suggested supporting file |
|---|---|---|---|
| E-01 | Local file hash | SHA-256: `8B9D1C0544FC19C927B4ADD91D48B122C74330F5F6759E2BD52E7FAA892DDEE3` | `screenshots/sha256.png` |
| E-02 | VirusTotal report | 0/65 detections at the time checked | `screenshots/virustotal-results.png` |
| E-03 | Manifest review | No `INTERNET` permission found in the inspection performed | `screenshots/jadx-manifest.png` |
| E-04 | Signature verification | APK v2 signature verification succeeded | `screenshots/signature-verification.png` |
| E-05 | Decompiled code | Notification-channel and rest-timer logic inspected | `screenshots/jadx-code.png` |
| E-06 | Device test | Main screens usable with Wi-Fi disabled / airplane mode enabled | `screenshots/offline-test.png` |
| E-07 | Android App info | No requested permissions shown; displayed data usage 0 B at the time checked | `screenshots/app-info.png` |

These screenshot filenames are placeholders for evidence I may add later. The screenshots are **not included** in this initial repository package.

## Evidence handling notes

- Keep an unmodified copy of the original APK outside this public repository.
- Record the date and tool version for future repeat tests.
- Redact personal notifications, account details, device identifiers, and unrelated files from screenshots.
- Do not publish the APK, private source code, or certificate details without permission.
- VirusTotal can retain or share uploaded samples under its own policies. Consider this before uploading private files.
