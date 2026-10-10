# Android APK Security Analysis

I wanted to get more practice with Android application security, so I analysed a small workout-tracking APK and documented what I checked, what I found, and what the results do and don't tell me.

The goal wasn't to prove that the app is perfectly safe. It was to practise a repeatable workflow using file hashing, reputation checking, APK signature verification, static analysis, and basic behaviour testing.

## Scope

- **App:** GymTracker
- **Package:** `com.laurikk.gymtracker`
- **Version:** `1.0`
- **File type:** Android APK
- **Tools:** PowerShell, VirusTotal, JADX, Android device settings, and Android APK signature verification tools
- **Testing:** Installed on a spare Android phone and checked core screens with Wi-Fi disabled / airplane mode enabled

> **Permission and privacy:** This analysis was performed for learning purposes. Before publishing screenshots, identifying details, or any app-specific findings, I will make sure I have the developer's permission. I am not including the APK or the developer's source code in this repository.

## Summary of findings

- SHA-256 was calculated locally and compared with the file shown in the VirusTotal report.
- VirusTotal showed **0/65 detections** in the report I checked.
- The APK's v2 signature verification succeeded.
- The manifest did not contain an `android.permission.INTERNET` permission in the inspection performed.
- I did not find obvious URL strings or common networking indicators in the searches I ran.
- The manifest declared permissions associated with vibration, notifications, and exact alarms.
- The app's main features remained usable during my offline test.
- The code I inspected included notification-channel setup and rest-timer notification handling, which appeared consistent with the app's stated workout-tracking functionality.

These are observations from the checks performed, not a guarantee that the APK is harmless. A clean reputation scan, lack of an Internet permission, a valid signature, and offline functionality each have limits.

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

## Reproduce the workflow

1. Work on a copy of the APK and record where it came from.
2. Calculate a SHA-256 hash.
3. Check the hash/file on a reputation service such as VirusTotal, considering privacy before uploading a sample.
4. Inspect the manifest and code in JADX.
5. Verify the APK signature with Android build tools.
6. Review permissions, components, URLs, networking code, storage behaviour, and any sensitive API use.
7. If dynamic testing is appropriate and authorised, use a spare device or isolated test environment and observe behaviour.
8. Record evidence and limitations, then write a conclusion proportional to the evidence.

## Hash recorded during this analysis

```text
8B9D1C0544FC19C927B4ADD91D48B122C74330F5F6759E2BD52E7FAA892DDEE3
```

Only use this hash to identify the exact file I examined. If the APK changes, its hash will change too.

## Conclusion

Based on the checks documented here, I did not identify clear evidence of malicious behaviour. I consider the result **low concern based on the available evidence**, not “proven safe.”

This was a learning exercise, not a formal security audit or a complete reverse-engineering assessment.
