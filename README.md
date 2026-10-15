# Swayambhu Monkey Chase: iOS and Android

This is the game wrapped as native iOS and Android apps with Capacitor. The game itself is `www/index.html`. The `android/` and `ios/` folders are real native projects you open in Android Studio and Xcode.

Already set up:
- Landscape only, full screen, screen stays awake.
- App icons and splash screens in every size.
- Fonts bundled, so the game works offline.
- Touch joystick and buttons always on.
- Haptic buzz on kicks, bells and when a monkey grabs your offerings.
- The game pauses when the app goes to the background.
- Android back button: pauses, then returns to the menu, then exits.

App ID: `com.swayambhu.monkeychase`. Change it in `capacitor.config.json` before you publish. On Android also change it in `android/app/build.gradle` and rename the Java package folder. On iOS change it under Signing & Capabilities.

## First time

You need Node.js 20 or newer.

```bash
npm install
npx cap sync
```

## Android

You need Android Studio, with its bundled JDK and the Android SDK.

1. Run `npm run android`. This syncs and opens the project in Android Studio.
2. Wait for Gradle to finish. Pick a phone or emulator and press Run.
3. For the Play Store, use **Build > Generate Signed Bundle / APK**, choose **Android App Bundle (.aab)** and create a keystore. Keep that keystore safe, because every future update must be signed with it.

To build a test APK from the command line instead:

```bash
cd android && ./gradlew assembleDebug
# output: android/app/build/outputs/apk/debug/app-debug.apk
```

## iOS

You need a Mac with Xcode 16 or newer. Swift Package Manager handles dependencies, so CocoaPods isn't needed.

1. Run `npm run ios`. This syncs and opens `ios/App/App.xcodeproj` in Xcode.
2. Select the **App** target, open **Signing & Capabilities** and choose your Team. A free Apple ID works for testing on your own phone.
3. Plug in an iPhone or pick a simulator and press Run.
4. For the App Store, use **Product > Archive**, then **Distribute App**. This needs a paid Apple Developer account.

## Changing the game

Edit `www/index.html`, then run `npx cap sync` and run again from Android Studio or Xcode.

To change the icon or splash, replace the files in `assets/`, then:

```bash
npm run assets
npx cap sync
```

## Store checklist

- Increase `versionCode` and `versionName` in `android/app/build.gradle`, and the version and build number in Xcode, on every release.
- Screenshots: landscape phone shots. Apple also wants iPad shots, because iPad is enabled.
- Privacy: the game collects no data. The best score is kept on the device only.
- Content rating: cartoon slapstick. Monkeys get shooed, never hurt.
