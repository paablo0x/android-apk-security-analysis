# Analysis Report: Android APK

## 1. Objective

I wanted to practise analysing an Android APK rather than relying only on a mobile antivirus result. I checked the file, inspected its manifest and decompiled code, verified its signature, and tested the app's normal functionality on a spare phone.

## 2. Sample details

| Field | Value |
|---|---|
| App name | GymTracker |
| Package | `com.laurikk.gymtracker` |
| Version | `1.0` |
| APK size | 3,804,226 bytes (local file listing) |
| SHA-256 | `8B9D1C0544FC19C927B4ADD91D48B122C74330F5F6759E2BD52E7FAA892DDEE3` |
| Minimum SDK | 28 |
| Target SDK | 37 |

The app was supplied by its developer for testing. The APK itself is not included in this repository.

## 3. Tools and methods

- **PowerShell:** calculated the file's SHA-256 hash.
- **VirusTotal:** checked the sample's reputation report.
- **JADX:** inspected the manifest and decompiled application code.
- **Android APK signature verification tools:** checked whether the APK signature verified.
- **Spare Android phone:** checked the app's normal screens and behaviour with Wi-Fi disabled / airplane mode enabled.

## 4. File hash and reputation

The SHA-256 hash recorded locally was:

`8B9D1C0544FC19C927B4ADD91D48B122C74330F5F6759E2BD52E7FAA892DDEE3`

The VirusTotal report I checked showed **0/65 detections**.

A clean VirusTotal result is useful context, but it is not proof that a file is safe. Detection results can change, and security products can miss new, targeted, or low-prevalence threats. Uploading files to third-party scanning services can also expose samples to the service and its sharing partners, so this should be considered before uploading private or confidential files.

## 5. Manifest and permissions

The package name shown in the manifest was `com.laurikk.gymtracker`, with version `1.0`.

The permissions observed included:

- `android.permission.VIBRATE`
- `android.permission.POST_NOTIFICATIONS`
- `android.permission.USE_EXACT_ALARM`
- `android.permission.SCHEDULE_EXACT_ALARM` (with a maximum SDK restriction in the manifest)

A custom permission was also present:

`com.laurikk.gymtracker.DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION`

During the manifest inspection, I did **not** find `android.permission.INTERNET`. I also searched for several permissions commonly worth reviewing during an initial triage, including SMS, microphone, contacts, location, overlay, accessibility-service, package-installation, and boot-completed permissions. Those searches did not return matches.

This is a limited permissions review, not a complete proof that the app cannot communicate externally or perform unwanted actions. I would still review every declared component, library, and code path in a deeper assessment.

## 6. Static code inspection

I opened the APK in JADX and reviewed the decompiled code.

Searches for obvious URL strings (`http://` and `https://`) and the `okhttp` string did not return matches in the searches performed. These searches can miss dynamically constructed URLs, obfuscated strings, other networking libraries, native code, or behaviour that is only triggered under certain conditions.

I also inspected some notification-related code. The application initialises notification channels named `rest_countdown` and `rest_over`. A receiver reads rest-timer information from an intent and builds a rest-completion notification that can open the main activity. The code I inspected looked consistent with a workout app's rest timer.

Some class and method names were obfuscated, so the decompiled output was not always easy to read. I did not complete a full review of every method or dependency.

## 7. APK signature

APK signature verification succeeded for the v2 signature.

The signing certificate displayed:

- **Subject:** `CN=Lauri Kuokka, O=GymTracker`
- **Signature algorithm:** SHA-384 with RSA
- **Public key:** RSA 4096-bit
- **Certificate validity shown:** 8 October 2026 to 23 February 2054
- **Certificate SHA-256 fingerprint:**

  `23 B6 25 DC 4F 9B 7D 93 4B 1A DB 04 21 F7 04 05 6E 3A 6B 33 0A A3 4A AA AE 04 EB 3B 64 B0 CB DE`

A valid APK signature means the APK's signed contents verify against the signing key. It does **not**, by itself, prove the real-world identity or trustworthiness of the person named in the certificate. I did not independently verify the certificate fingerprint with the developer through a separate trusted channel.

## 8. Dynamic / device testing

I installed the app on a spare Android phone and checked the main tabs and screens, including the workout dashboard, programs, history, body/profile setup, and exercise list.

I also enabled airplane mode and checked that the main areas remained usable with Wi-Fi off. The Android App info screen showed no requested permissions, and the displayed data usage was 0 B at the time I checked.

This supports the observation that the app's main functionality can work offline. It does not prove that the app never attempts network access or that no code is triggered only after a particular action, time, or device state. The test was manual and limited in duration.

## 9. Findings

| Check | Observation | Interpretation |
|---|---|---|
| SHA-256 | Hash recorded locally and compared with the report | Helps identify the exact sample |
| VirusTotal | 0/65 detections in the report checked | Reassuring signal, not a guarantee |
| APK signature | v2 verification succeeded | Signed contents verified against the included signing key |
| Manifest | No `INTERNET` permission found in inspection | No normal manifest-declared Internet permission observed |
| String searches | No obvious URL or `okhttp` matches | Limited search only; not exhaustive |
| Permissions | Vibration, notifications, exact-alarm permissions observed | Broadly consistent with workout/rest-timer features |
| Code review | Notification-channel and rest-timer logic inspected | The code reviewed appeared consistent with app functionality |
| Offline test | Main screens worked with Wi-Fi disabled | Main features appeared usable offline during testing |

## 10. Limitations

- I did not review every line of decompiled code.
- Decompiled output can be incomplete or difficult to interpret, especially when names are obfuscated.
- String searches can miss encoded or dynamically constructed values.
- I did not perform a full dynamic analysis with traffic interception, system-call monitoring, or long-duration observation.
- I did not exhaustively inspect every third-party library or native library.
- A valid signature does not establish that the developer is trustworthy.
- VirusTotal results represent the engines and detections available at the time of the check.
- Manual offline testing cannot prove that the app never communicates externally.

## 11. Conclusion

I did not identify clear indicators of malicious behaviour in the checks I performed. The permissions and the notification code I inspected appeared consistent with the app's workout-tracking functionality, and the app's main screens worked during my offline test.

My assessment is **low concern based on the evidence collected**, not a certification that the APK is safe. A deeper assessment would include a more complete code review, inspection of all components and dependencies, and controlled monitoring of the app's runtime behaviour.
