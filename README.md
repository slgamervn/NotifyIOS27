# NotifyIOS27

**iOS-style notification banners and Dynamic Island for Android.**

NotifyIOS27 brings clean, floating notification banners and a Dynamic Island-style overlay to any Android device. It listens to your notifications and displays them in a modern, non-intrusive way — inspired by iOS — while staying fully customizable.

## Features

- **Floating notification banners** — Smooth, glass-style banners that appear over other apps
- **Dynamic Island** — Compact pill-shaped overlay for ongoing activities and notifications
- **Focus modes** — Temporary rules to silence or prioritize apps
- **Notification history & stats** — Review past notifications and usage
- **Filters & rules** — Control which apps trigger banners or island
- **Quick Settings tiles** — Toggle banner, focus, and island from the shade
- **Home screen widget** — Quick access and status
- **Backup & restore** — Export/import your settings
- **Onboarding flow** — Guided permission setup

## Requirements

- Android 8.0 (API 26) or higher
- Permissions:
  - Notification access (`NotificationListenerService`)
  - Display over other apps (`SYSTEM_ALERT_WINDOW`)
  - Post notifications (Android 13+)

## Installation

### From GitHub Releases
1. Go to the [Releases](https://github.com/slgamervn/NotifyIOS27/releases) page
2. Download the latest `notifyIOS27-release.apk` (or debug if needed)
3. Enable “Install unknown apps” for your browser/file manager
4. Install and open the app
5. Follow the onboarding to grant Notification access and Display over other apps

### Build from source

The project is packaged as `app.zip` for GitHub Actions builds.

Requirements: JDK 17, Android SDK, and system Gradle 8.14.2.

```bash
unzip app.zip -d proj
cd proj
gradle --version
gradle assembleDebug --no-daemon
```

The source archive does not include a Gradle Wrapper. The GitHub Actions workflow installs and verifies Gradle 8.14.2. Release signing is controlled by the repository workflow; do not create or replace a signing key casually.

APK outputs:
- `app/build/outputs/apk/debug/notifyIOS27-debug.apk`
- `app/build/outputs/apk/release/notifyIOS27-release.apk`

## Updates and releases

The Android build is split into a test path and a production-release path:

1. Push an updated `app.zip` to `dev`. GitHub Actions builds both APK variants, checks that they use the same application ID, version metadata, and signing certificate, then uploads a short-lived Actions artifact. It does **not** create a public Release.
2. Open a pull request from `dev` to `main`. The same build checks run on the pull request. Review the result before merging.
3. Merge the tested `app.zip` change into `main` only after the signing migration is reviewed and the publication gate can pass. The workflow currently blocks Release publication while signing keystore material is tracked in the repository; a green build on `dev` or a pull request is an artifact-only test, not a public Release.
4. Manual workflow runs are build-only by default. The optional publish switch is available only when the workflow is run from `main`.

Each Release contains:
- `notifyIOS27-release.apk` — release variant
- `notifyIOS27-debug.apk` — debug/testing variant
- `SHA256SUMS.txt` — checksums for both APK files

The in-app updater only accepts the official HTTPS GitHub Release APK URL. Before opening Android's package installer, it downloads the matching `SHA256SUMS.txt`, verifies the release APK's SHA-256 digest, checks the download size, and rejects incomplete or mismatched files. Android then performs its own package/signature compatibility checks.

Before installing an update, Android requires the same application ID and compatible signing identity, and the update's `versionCode` must be higher than the installed version. Keep the application ID and signing identity stable, and increase `versionCode` for every update. The workflow verifies each APK against its own previously published variant: the debug APK is compared with the previous debug APK, and the release APK with the previous release APK. Debug and release may use different signing certificates; do not switch an installation between variants. A successful CI check does not replace device-level installation testing.

### Signing-key limitation

The current workflow restores a fixed, repository-shared **debug signing key** so existing installations can continue to accept updates. Android's documentation states that debug certificates are insecure by design and are not appropriate as a production app-signing identity. This key material is committed to the public repository and must be treated as compromised; deleting it from the current branch would not remove it from Git history. These APKs are therefore test/distribution builds, not securely authenticated production releases or Play Store builds. The workflow now blocks Release publication while recognized signing keystore files remain tracked. Do not remove or rotate the existing key casually: doing so can make already-installed copies reject future updates. The migration plan is tracked in [issue #2](https://github.com/slgamervn/NotifyIOS27/issues/2).

### Backup limitations

The built-in backup is **not a full app backup**. It currently exports only a limited subset of preferences. It does not include the on-device notification store, the notification-history database, custom wallpaper files, or separate health/island preference stores. Android permission grants and OS-scheduled work also cannot be restored as app data and must be set up again after reinstalling. Do not rely on the current export alone to migrate every local item to a separately signed installation; the complete transfer plan is tracked in [issue #2](https://github.com/slgamervn/NotifyIOS27/issues/2).

## Usage

1. Grant the required permissions during onboarding
2. Open the app and configure:
   - Banner style & position
   - Island appearance and sources
   - Focus rules
   - Per-app filters
3. Incoming notifications will appear as banners or in the Island according to your settings
4. Swipe or tap to dismiss / open the original notification

## Privacy

All processing happens on-device.  
Notification content is only used to display banners/island and is not sent to any server.

## License

Source code is not open source.  
See repository description for details.

## Credits

Built with Kotlin and AndroidX.  
UI inspired by iOS notification and Dynamic Island design language.
