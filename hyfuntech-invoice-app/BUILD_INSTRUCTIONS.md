# Hyfuntech Invoice — Android App

This is a complete, ready-to-build Android project for your Invoice
Management System. It's a native app shell that opens
**https://invoice.hyfuntech.com** in a full-screen WebView — your app icon,
your app name, your splash screen, no browser address bar.

I could not compile this into a final `.apk` file myself (explained below),
but the actual build step takes about 2 minutes on your end.

## Why I'm handing you a project instead of a finished .apk

Building an Android app requires downloading the Android SDK and Gradle's
dependencies from Google's servers (`dl.google.com`, `maven.google.com`) and
Maven Central. The sandboxed environment I work in has network access
restricted to a specific allow-list (npm, GitHub, PyPI, Ubuntu's package
repos) for security reasons, and none of those Android build servers are on
it — I checked directly rather than assuming. Your own computer won't have
this restriction, so the build "just works" there.

## How to build the APK (pick one)

### First, one-time setup
This project doesn't include its `node_modules` folder (standard practice —
it's large and easily regenerated). Before opening it in Android Studio,
install [Node.js](https://nodejs.org) if you don't have it, then in this
project's root folder run:
```
npm install
```

### Option A: Android Studio (recommended, easiest)
1. Install [Android Studio](https://developer.android.com/studio) (free) if you don't have it.
2. Open Android Studio → **Open** → select the `android` folder inside this project.
3. Let it sync (first time may take a few minutes — it's downloading the SDK).
4. Menu: **Build → Build App Bundle(s) / APK(s) → Build APK(s)**.
5. When it finishes, click the **"locate"** link in the notification, or find
   it at `android/app/build/outputs/apk/debug/app-debug.apk`.
6. Copy that file to your Android phone (email, USB, Google Drive, whatever)
   and tap it to install. You'll need to allow "Install from unknown
   sources" the first time — Android will prompt you for this automatically.

### Option B: Command line (if you have Android SDK + Java already)
```
cd android
./gradlew assembleDebug
```
Output lands in the same place: `android/app/build/outputs/apk/debug/app-debug.apk`

## Important: this is a DEBUG build

The steps above produce a debug APK — perfect for installing on your own
phone and testing right now. If you ever want to:
- **Publish it on the Google Play Store**, or
- **Distribute it to other people's phones long-term**

...you'll need a signed **release** build instead (Android Studio: **Build →
Generate Signed Bundle / APK**, which walks you through creating a signing
key). Debug builds work fine for personal/internal use but aren't meant for
public distribution.

## What's already configured
- App name: **Hyfuntech Invoice**
- Package ID: `com.hyfuntech.invoice`
- Points to: `https://invoice.hyfuntech.com`
- App icon + splash screen: generated from your uploaded logo, in every
  required Android resolution (mdpi through xxxhdpi, plus round icon
  variants and light/dark splash screens)
- Internet permission: already added (required since the app loads a live website)

## If you ever change your domain or app name later
Edit `capacitor.config.json` in this project's root, then re-run:
```
npx cap sync android
```
That regenerates the Android project's runtime config without needing to
redo anything else.
