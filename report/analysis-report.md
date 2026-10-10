# Analysis Report: Anonymized Android APK

## 1. Objective

I wanted to practise analysing an Android APK rather than relying only on a mobile antivirus result. I checked the file, inspected its manifest and decompiled code, verified its signature, and tested normal functionality on a spare phone.

This report has been anonymized. It intentionally omits the original app name, package identifier, exact file hash, signing-certificate identity and fingerprint, exact report links, and identifying screenshots.

## 2. Sample details

| Field | Published value |
|---|---|
| App | Anonymized workout-tracking app |
| Version | 1.0 (as observed during testing) |
| File type | Android APK |
| File hash | Withheld to avoid linking the report to the original file |
| SDK details | Omitted from this public version |

The sample was made available for testing. The APK and its source code are not included in this repository.

## 3. Tools and methods

- **PowerShell:** calculated the file's SHA-256 hash locally.
- **VirusTotal:** checked the sample's reputation report.
- **JADX:** inspected the manifest and decompiled application code.
- **Android APK signature verification tools:** checked whether the APK signature verified.
- **Spare Android phone:** checked the app's normal screens and behaviour with Wi-Fi disabled / airplane mode enabled.

## 4. File hash and reputation

I calculated a SHA-256 hash locally and compared the file with a VirusTotal report. The exact hash, report URL, and sample-identifying details are intentionally not published.

The report I checked showed no detections at the time. A clean VirusTotal result is useful context, but it is not proof that a file is safe. Detection results can change, and security products can miss new, targeted, or low-prevalence threats. Uploading files to third-party scanning services can also expose samples to the service and its sharing partners, so this should be considered before uploading private or confidential files.

## 5. Manifest and permissions

During manifest inspection, I did not find `android.permission.INTERNET`. The permissions I observed included permissions associated with vibration, notifications, and exact alarms. A custom permission associated with receiver handling was also present.

I searched for several permissions commonly worth reviewing during initial triage, including SMS, microphone, contacts, location, overlay, accessibility-service, package-installation, and boot-completed permissions. Those searches did not return matches.

This is a limited permissions review, not proof that an app cannot communicate externally or perform unwanted actions. A deeper assessment would review every declared component, library, and code path.

## 6. Static code inspection

I opened the APK in JADX and reviewed the decompiled code.

Searches for obvious URL strings (`http://` and `https://`) and a common networking-library string did not return matches in the searches performed. These searches can miss dynamically constructed URLs, obfuscated strings, other networking libraries, native code, or behaviour that is only triggered under certain conditions.

I also inspected notification-related code. The application initialised notification channels and included a receiver that handled rest-timer information and built a rest-completion notification. The code I inspected appeared consistent with the stated workout-tracking functionality.

Some class and method names were obfuscated, so the decompiled output was not always easy to read. I did not complete a full review of every method or dependency.

## 7. APK signature

APK signature verification succeeded for the signature scheme checked. The certificate's subject, fingerprint, validity dates, and other identifying details are intentionally omitted from this public report.

A valid APK signature means the signed contents verify against the signing key. It does **not**, by itself, prove the real-world identity or trustworthiness of the person who signed the APK. I did not independently verify the signing key through a separate trusted channel.

## 8. Dynamic / device testing

I installed the app on a spare Android phone and checked its main areas, including the workout dashboard, programs, history, profile setup, and exercise list.

I also enabled airplane mode and checked that the main areas remained usable with Wi-Fi off. At the time I checked, Android's app information screen showed no requested permissions and displayed zero data usage.

This supports the observation that the app's main functionality can work offline. It does not prove that the app never attempts network access or that no code is triggered only after a particular action, time, or device state. The test was manual and limited in duration.

## 9. Findings

| Check | Observation | Interpretation |
|---|---|---|
| File identity | SHA-256 calculated locally; exact value withheld | Helps identify the sample during analysis without publishing its fingerprint |
| Reputation | No detections in the report checked at the time | Reassuring signal, not a guarantee |
| APK signature | Signature verification succeeded | Signed contents verified against the signing key |
| Manifest | No `INTERNET` permission found in the inspection performed | No normal manifest-declared Internet permission observed |
| String searches | No obvious URL strings found in searches performed | Limited search only; not exhaustive |
| Permissions | Vibration, notification, and exact-alarm permissions observed | Broadly consistent with workout/rest-timer features |
| Code review | Notification and rest-timer logic inspected | The code reviewed appeared consistent with app functionality |
| Offline test | Main screens worked with Wi-Fi disabled | Main features appeared usable offline during testing |

## 10. Limitations

- I did not review every line of decompiled code.
- Decompiled output can be incomplete or difficult to interpret, especially when names are obfuscated.
- String searches can miss encoded or dynamically constructed values.
- I did not perform a full dynamic analysis with traffic interception, system-call monitoring, or long-duration observation.
- I did not exhaustively inspect every third-party library or native library.
- A valid signature does not establish that the developer is trustworthy.
- Reputation results represent the engines and detections available at the time of the check.
- Manual offline testing cannot prove that the app never communicates externally.

## 11. Conclusion

I did not identify clear indicators of malicious behaviour in the checks I performed. The permissions and notification code I inspected appeared consistent with the app's workout-tracking functionality, and the app's main screens worked during my offline test.

My assessment is **low concern based on the evidence collected**, not a certification that the APK is safe. A deeper assessment would include a more complete code review, inspection of all components and dependencies, and controlled monitoring of runtime behaviour.
