# Findings and quick notes

These are my working notes from the APK analysis. The full report is in [`../report/analysis-report.md`](../report/analysis-report.md). Identifying details have been removed from this public version.

## Checks performed

- [x] Calculated SHA-256 locally (exact value withheld)
- [x] Checked a VirusTotal report (exact report details withheld)
- [x] Opened the APK in JADX
- [x] Reviewed the manifest and permissions
- [x] Searched for common sensitive permissions
- [x] Searched for obvious URL strings and a common networking-library string
- [x] Verified the APK signature
- [x] Inspected some notification and rest-timer code
- [x] Installed on a spare Android phone
- [x] Tested main screens with Wi-Fi disabled / airplane mode enabled

## Main observations

- I did not find the `android.permission.INTERNET` permission in the manifest inspection.
- I did not find obvious URL strings in the searches I ran.
- The permissions I observed included vibration, notifications, and exact alarms.
- The notification code I reviewed appeared consistent with a rest timer.
- The app's main screens remained usable during my offline test.
- Nothing suspicious stood out in the parts I checked.

## Assessment

**Low concern based on current evidence.** This is not proof that the app is harmless. The analysis was limited, and I did not fully review every code path or monitor all runtime activity.
