# Capture (For Therapists) - Privacy Policy & Data Deletion

*Last updated: May 2026*

## Overview

Capture is an offline-first practice management app for mental health professionals. All clinical data is stored locally on your device. There is no Capture-operated server holding client records. Optional encrypted backup to Google Drive or a local folder is the only way data leaves the device, and only by your explicit choice.

## Information We Collect

### Clinical data (stored locally only)

Everything you enter, including client profiles, case histories, follow-up sessions, treatment goals, assessments, attachments, payments, audio recordings, and exported PDFs, is stored in Capture's private storage on your device. This data never leaves your device unless you explicitly choose to back it up. Capture has no server to send it to.

### Optional encrypted backup

You may choose to back up your data to your own Google Drive or to a local folder on your device. If you do, the data is AES-256 encrypted on this device before being written. The encryption key is derived from a backup PIN that you set, separate from the device unlock that gates access to the app. Capture does not have a copy of your backup PIN. The encrypted file is stored at the destination you pick (Google Drive or a folder you select), not on any server controlled by the developer.

### Anonymous usage analytics

Capture collects anonymous usage analytics (which features get used, app version, broad properties about your account) to help improve the app. Analytics never include client names, session content, case-history text, attachment contents, audio, or any identifying information. You can disable analytics at any time in Settings, "Help improve Capture". Doing so immediately stops collection, deletes your analytics profile from the analytics provider, and clears locally stored analytics state.

### Location data

Capture does not collect any location information.

## Third-Party Access

No clinical data is shared with any third party. The only outbound traffic from Capture is anonymous usage analytics (described above), which can be disabled. If you opt into Google Drive backup, the encrypted file goes to your own Drive account and is governed by your relationship with Google, not Capture.

## Security and HIPAA Alignment

### Why we say "HIPAA-aligned" and not "HIPAA-compliant"

HIPAA compliance is achieved by a covered entity (the therapist's practice), not by an app. An app can implement the technical safeguards that HIPAA's Security Rule describes; it cannot deliver a Notice of Privacy Practices to a client on the therapist's behalf, file a breach report with HHS, or sign a Business Associate Agreement with a third-party storage provider. Calling Capture "HIPAA-compliant" would imply that using the app, alone, satisfies HIPAA. It does not, and we do not claim that. "HIPAA-aligned" draws the line honestly: the technical foundation is in the app, the practice itself is yours to run.

### What Capture implements

Capture implements the technical safeguards described in 45 CFR §164.312, supported by parts of §164.308 and §164.316:

- **§164.312(a)(1) Access control and §164.312(d) Person or entity authentication**: Capture requires a device lock screen to run; on a device with no lock screen, the app blocks startup. Access is gated by the device's biometric prompt, with the device credential (PIN, pattern, password) as the system fallback. Sensitive actions, such as Wipe All Data, require an additional one-shot biometric prompt that bypasses the session window.
- **§164.312(a)(2)(iii) Automatic logoff**: after 15 minutes of inactivity in the foreground, or after the app has been backgrounded for 15 minutes, Capture re-prompts for authentication on return. The same idle lock applies to ORS and SRS client-handoff screens; if a client takes longer than 15 minutes on a form, the lock screen appears and the therapist re-authenticates before the session can continue.
- **§164.312(a)(2)(iv) Encryption and decryption**: the local database is AES-256 encrypted at rest via SQLCipher. The database passphrase is wrapped with an AES-256 GCM key stored in the device's Android Keystore (hardware-backed where the device provides one). Optional backups are AES-256 encrypted before they leave the device, using a PBKDF2-derived key from the backup PIN you set.
- **§164.312(b) Audit controls**: Capture records create, update, delete, view, export, backup, restore, wipe, authentication-success, authentication-failure, encryption-failure, retention-prune, acknowledge, and EULA-acceptance events. The log is reviewable in Settings, "Activity log" and exportable as CSV. See "Audit Log" below for details.
- **§164.308(a)(7) Contingency plan**: a first-launch flow guides you to a recovery destination (Google Drive, a local folder, or deferred), so a backup exists in case of device loss. A contingency plan template is included in-app under Settings, "HIPAA Documents".
- **§164.316(b)(2)(i) Time limit**: §164.316 requires security-policy documentation to be retained for six years; (b)(2)(i) is the time-limit sub-spec. The audit log is the record of activity on those policies, so when you Wipe All Data, Capture first asks you to save a CSV copy of the activity log to a destination you pick; the wipe does not proceed until that copy is written.

### What stays your responsibility

The administrative, organisational, and operational requirements of HIPAA cannot be implemented by an app. Capture provides templates for several of them under Settings, "HIPAA Documents", but delivery, sign-off, and reporting are yours:

- **§164.520 Notice of Privacy Practices**: a template is provided in-app as a read-only reference. You should adapt it for your practice outside the app and deliver the adapted version to clients at intake; obtaining their acknowledgment is your responsibility. Before the first PDF Export for a given client, Capture shows a Notice-of-Privacy-Practices acknowledgment dialog. Confirming it persists a Privacy Notice consent record for that client, after which subsequent PDF exports for the same client skip the dialog. The Share-the-exported-PDF flow does not have its own consent gate; it relies on the consent captured at Export time. You can view or revoke this consent at any time under Manage Consent on the client's profile, alongside Treatment, Audio Recording, and Telehealth consents.
- **§164.308(a)(1)(ii)(A) Risk analysis** and the broader security management process: a template is provided. Completing, signing, and storing the document is your responsibility.
- **§164.400 through §164.414 Breach notification**: a breach notification procedure template is provided. Filing reports with HHS and notifying affected clients within the legal timeframe is your responsibility.
- **§164.308(b)(1) and §164.314(a) Business Associate Agreements**: if you back up to Google Drive, the BAA requirement applies to that storage relationship. Google offers a BAA to certain Google Workspace plans and does not offer one for personal Gmail accounts. Verify directly with Google whether your specific account qualifies. The local-folder backup option avoids this question entirely.
- **§164.310 Physical safeguards**: device security (a strong device PIN, OS updates, not sharing or leaving the device unattended) is your responsibility.
- **§164.524 Right to access**, **§164.526 Right to amend**, and **§164.528 Accounting of disclosures**: the audit log gives you the raw material to compile an accounting; producing the formal response to a client request is your responsibility.

### Why this matters when choosing a backup destination

- **Google Drive backup**: the encrypted file goes to your own Drive account. Google cannot read its contents. HIPAA's BAA requirement still attaches to Google as a storage provider, and is yours to evaluate.
- **Local folder backup**: the encrypted file stays on a device or folder you control. No third party is in the picture; the BAA question does not arise.

Either choice is supported.

## Audit Log

### What gets logged

Every create, update, delete, view, export, backup, restore, wipe, authentication success, authentication failure, encryption-failure, retention-prune, acknowledge, and EULA-acceptance event is recorded. PDF disclosures additionally record the channel used to deliver the password (SMS, clipboard, or manual) and the recipient you entered when you choose to enter one, to give you the raw material for a §164.528 accounting of disclosures.

### Where it lives

The audit log lives inside Capture's AES-256 encrypted database on your device. It is not a separately tamper-proof log; it is encrypted at the same level as your clinical data.

### How to export it

- **Anytime**: Settings, "Activity log" lets you review entries and export the full log to a CSV file at a destination you pick.
- **Before a wipe**: Settings, "Wipe All Data" will ask you to save a CSV copy of the audit log before the wipe proceeds. The wipe does not start until the export is written. If you cancel the export, the wipe is cancelled too.

## Automatic Logoff

Per §164.312(a)(2)(iii), Capture re-prompts for authentication after 15 minutes of inactivity in the foreground, and after the app has been backgrounded for 15 minutes. The threshold is the same in both directions.

## Data Deletion

### Delete individual records

Within the app, you can delete individual client profiles, follow-up sessions, treatment goals, assessments, and other records using the delete option on each record. Each deletion is logged in the activity log per §164.312(b).

### Delete all app data

Settings, "Wipe All Data" requires a fresh biometric prompt. Before the wipe proceeds, Capture asks you to save a CSV copy of the activity log to a destination you pick (§164.316(b)(2)(i) six-year retention). When you confirm the wipe:

- background jobs are cancelled;
- every database row, the database files themselves, every locally stored audio recording, every cached PDF, every temporary backup, and every preferences file is removed;
- the Android Keystore entry that wrapped your database encryption key is destroyed in a `finally` block so that even if an earlier step throws, the wrapping key is gone and any residual scrambled bytes on disk are unreadable (§164.310(d)(2)(i) disposal).

### Uninstall

Uninstalling Capture removes all locally stored Capture data from your device.

### Delete Google Drive backups

If you used the Google Drive backup option, your backup is in your own Google Drive account. To delete it, open Google Drive, locate the Capture backup file, and delete it. Capture does not retain any copy.

### Delete local-folder backups

If you chose a local folder for backup, delete the file from that location using your phone's file manager.

### Disable and delete analytics data

Go to Settings, "Help improve Capture" and turn the toggle off. This will:

- immediately stop all future analytics collection;
- delete your analytics profile from the analytics provider's servers;
- clear all locally stored analytics data.

You can re-enable analytics at any time from the same setting.

### No remote clinical data to delete

Capture does not transmit or store your clinical data on any server. There is no remote clinical data to request deletion of. All clinical data resides solely on your device and, if you chose to enable it, in the backup destination you control.

## Changes

This policy may be updated from time to time. Changes will be posted on this page. Continued use of the app after changes are posted constitutes acceptance of the updated policy.

## Contact

If you have questions about privacy or data deletion, contact us at reflections.dreams.memories@gmail.com.
