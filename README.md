# Dekanto Android App

Android wrapper application for [dekanto.rs](https://dekanto.rs) built with Capacitor.

## Overview

This is a native Android application that wraps the Dekanto web application (Vue.js frontend + Laravel backend) using Capacitor, allowing it to be distributed and installed as a standalone mobile app.

## Prerequisites

- Node.js (v14 or higher)
- Java JDK 21 (Eclipse Adoptium recommended)
- Android SDK (automatically downloaded during build)

## Project Structure

```
dekanto_app/
├── android/                 # Native Android project
│   ├── app/                # Android app module
│   └── gradle/             # Gradle wrapper files
├── www/                    # Web assets
│   └── index.html         # Entry point that loads dekanto.rs
├── capacitor.config.json   # Capacitor configuration
├── package.json           # Node.js dependencies
└── .gitignore            # Git ignore rules
```

## Setup

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd dekanto_app
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Ensure Java 21 is installed:**
   ```bash
   java -version
   # Should show: openjdk version "21.0.x"
   ```

## Building the APK

### Debug Build (for testing)

```bash
cd android
./gradlew assembleDebug
```

The APK will be generated at:
```
android/app/build/outputs/apk/debug/app-debug.apk
```

### Release Build (for production)

```bash
cd android
./gradlew assembleRelease
```

**Note:** Release builds require signing configuration. See [Android App Signing](https://developer.android.com/studio/publish/app-signing) for details.

## Installing on Device

### Method 1: ADB (Android Debug Bridge)
```bash
adb install android/app/build/outputs/apk/debug/app-debug.apk
```

### Method 2: Manual Transfer
1. Copy the APK file to your Android device
2. Open the APK file on your device
3. Follow the installation prompts

**Note:** You may need to enable "Install from Unknown Sources" in your device settings.

## Configuration

### App Details

- **Package ID:** `com.dekanto.app`
- **App Name:** Dekanto App
- **Target SDK:** Android 14 (API 35)
- **Minimum SDK:** Android 6.0 (API 23)

### Web App URL

The app loads the production website from:
```
https://dekanto.rs
```

To change this, edit `capacitor.config.json`:
```json
{
  "server": {
    "url": "https://your-domain.com"
  }
}
```

And update `www/index.html` if needed.

## Development

### Sync Changes

After modifying web assets or configuration:
```bash
npx cap sync android
```

### Open in Android Studio

```bash
npx cap open android
```

This allows you to:
- Use the visual layout editor
- Debug with breakpoints
- Run on emulators
- Build release versions with signing

## Updating Capacitor

```bash
npm install @capacitor/core@latest @capacitor/cli@latest @capacitor/android@latest
npx cap sync
```

## Troubleshooting

### Build Fails with Java Version Error

Make sure Java 21 is installed and set as JAVA_HOME:
```bash
export JAVA_HOME="/path/to/jdk-21"
export PATH="$JAVA_HOME/bin:$PATH"
```

Or on Windows:
```cmd
set JAVA_HOME=C:\Program Files\Eclipse Adoptium\jdk-21.x.x-hotspot
```

### APK Install Fails

1. Enable USB Debugging on your device
2. Enable "Install from Unknown Sources"
3. Check that the APK is not corrupted (re-download if needed)

### Web App Doesn't Load

1. Check your internet connection
2. Verify the URL in `capacitor.config.json` is correct
3. Ensure https://dekanto.rs is accessible

## Adding Features

### App Icon

Replace the icon files in:
```
android/app/src/main/res/mipmap-*/ic_launcher.png
```

### Splash Screen

Replace splash images in:
```
android/app/src/main/res/drawable-*/splash.png
```

### Native Plugins

Install Capacitor plugins for native features:
```bash
npm install @capacitor/camera
npx cap sync
```

See [Capacitor Plugins](https://capacitorjs.com/docs/plugins) for available options.

## License

[Your License Here]

## Support

For issues related to:
- **The web app:** Contact the Dekanto team
- **The Android wrapper:** Create an issue in this repository

## Built With

- [Capacitor](https://capacitorjs.com/) - Cross-platform native runtime
- [Android](https://developer.android.com/) - Mobile platform
- [Vue.js](https://vuejs.org/) - Web frontend (dekanto.rs)
- [Laravel](https://laravel.com/) - Web backend (dekanto.rs)
