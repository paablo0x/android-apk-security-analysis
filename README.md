# Android APK Security Analysis

I wanted to get more practice with Android application security, so I analysed a sample workout-tracking APK and documented the checks I performed, the observations I made, and the limits of the results.

This repository is an **anonymized learning case study**. App-specific identifiers, hashes, certificate details, screenshots, and other information that could identify the developer or link to the original file have been removed. The original APK and source code are not included.

## Scope

- **Sample:** An anonymized Android workout-tracking app
- **Tools:** PowerShell, VirusTotal, JADX, Android device settings, and Android APK signature verification tools
- **Testing:** Installed on a spare Android phone and checked core screens with Wi-Fi disabled / airplane mode enabled

## Summary of observations

- I calculated a SHA-256 hash locally to identify the exact file during testing. The value is intentionally not published.
- A VirusTotal report checked during the analysis showed no detections at that time. The exact report and identifying indicators are not included.
- APK signature verification succeeded.
- I did not find the `android.permission.INTERNET` permission during the manifest inspection.
- I did not find obvious URL strings in the searches I ran.
- The manifest included permissions associated with vibration, notifications, and exact alarms.
- The app's main features remained usable during my offline test.
- Some notification and rest-timer code I inspected appeared consistent with a workout-tracking app.

These are observations from limited checks, not a guarantee that the APK is harmless. A clean reputation scan, lack of an Internet permission, a valid signature, and offline functionality each have limits.

## Repository contents

```text
.
├── README.md
├── report/
│   └── analysis-report.md
├── notes/
│   ├── findings.md
│   └── evidence-log.md
├── screenshots/
│   └── README.md
└── .gitignore
```

## Workflow

1. Work on a copy of the APK and record where it came from.
2. Calculate a SHA-256 hash locally. Keep the value private if publishing it could identify the sample.
3. Check the sample with a reputation service such as VirusTotal, considering privacy before uploading it.
4. Inspect the manifest and code in JADX.
5. Verify the APK signature with Android build tools.
6. Review permissions, components, URLs, networking code, storage behaviour, and sensitive API use.
7. If dynamic testing is appropriate and authorised, use a spare device or isolated test environment and observe behaviour.
8. Record evidence and limitations, then write a conclusion proportional to the evidence.

## Conclusion

Based on the checks documented here, I did not identify clear evidence of malicious behaviour. I consider the result **low concern based on the available evidence**, not “proven safe.”

This was a learning exercise, not a formal security audit or a complete reverse-engineering assessment. The report has been anonymized to avoid identifying the app's developer or original APK.
