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

```bash
# Unzip and build locally
unzip app.zip -d proj
cd proj
./gradlew assembleRelease
```

APK outputs:
- `app/build/outputs/apk/debug/notifyIOS27-debug.apk`
- `app/build/outputs/apk/release/notifyIOS27-release.apk`

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
