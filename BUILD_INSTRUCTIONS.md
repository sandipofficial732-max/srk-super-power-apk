# SRK Super Power APK - Build Instructions

## Prerequisites

1. **Node.js & npm** (v14+)
   - Download: https://nodejs.org/
   - Verify: `node --version` and `npm --version`

2. **Android Studio**
   - Download: https://developer.android.com/studio
   - Install Android SDK (API 30+)
   - Set ANDROID_HOME environment variable

3. **Java Development Kit (JDK 11+)**
   - Included with Android Studio, or download separately

---

## Quick Build Steps

### 1. Install Dependencies
```bash
npm install
```

### 2. Initialize Capacitor (First Time Only)
```bash
npm run cap:init
```
When prompted:
- App name: `SRK Super Power`
- Bundle ID: `com.srk.superpower`

### 3. Add Android Platform (First Time Only)
```bash
npm run cap:add:android
```

### 4. Build Web Assets
```bash
npm run build
```

### 5. Sync to Android
```bash
npm run cap:sync
```

### 6. Open in Android Studio
```bash
npm run cap:open:android
```

---

## Build APK in Android Studio

1. Android Studio will open with the `android` folder
2. Wait for Gradle to sync (bottom-right notification)
3. Go to **Build → Build Bundle(s) / APK(s) → Build APK(s)**
4. Choose `debug` for testing or `release` for production
5. APK will be generated in: `android/app/build/outputs/apk/`

---

## Build Release APK (Production)

### Generate Signing Key
```bash
keytool -genkey -v -keystore srk-superpower.keystore -keyalg RSA -keysize 2048 -validity 10000 -alias srk-app
```

### Sign in Android Studio
1. **Build → Generate Signed Bundle / APK**
2. Select **APK**
3. Choose the keystore file you created
4. Build type: **Release**
5. Click **Finish**

Your signed APK will be in `android/app/build/outputs/apk/release/`

---

## Troubleshooting

### Camera Not Working
- Ensure `AndroidManifest.xml` has camera permissions:
  ```xml
  <uses-permission android:name="android.permission.CAMERA" />
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
  <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
  ```

### Geolocation Errors
- Grant location permission when app prompts
- Check your device's location settings are enabled

### Gradle Sync Fails
- Update Android Studio to latest version
- Delete `android/.gradle` folder and retry
- Check Java version: `java -version` should be 11+

---

## Testing APK

### On Android Device
```bash
# Install debug APK
adb install android/app/build/outputs/apk/debug/app-debug.apk
```

### Via USB
1. Connect Android device via USB
2. Enable USB Debugging in Developer Options
3. In Android Studio: **Run → Run 'app'**

---

## App Permissions Required

The app requests:
- **Camera** - for face registration and attendance
- **Location** - to verify office location
- **Storage** - for localStorage (local database)

All permissions are prompted at runtime on Android 6+.

---

## Additional Resources

- Capacitor Docs: https://capacitorjs.com/docs
- Android Studio Guide: https://developer.android.com/studio/intro
- Face-API.js Docs: https://github.com/vladmandic/face-api
