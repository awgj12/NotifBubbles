# Notification Bubbles

Floating notification bubbles for Android 10+ (built with the Nothing Phone 3a in mind), in a Nothing OS inspired style.
This is an independent project, not made or endorsed by Nothing.

## Get the APK

1. Create a GitHub repository and upload everything in this folder to its `main` branch,
   including the hidden `.github` folder.
2. Open the **Actions** tab and wait for **Build APK** to finish. You can also start it with **Run workflow**.
3. Download it either way:
   - **Releases** (easiest on a phone): open the newest release and tap `app-debug.apk`.
   - **Actions artifact:** open the run and download `NotificationBubbles-debug-apk` (a zip containing the APK; requires sign-in).

Inside the build, the APK is at `app/build/outputs/apk/debug/app-debug.apk`.
In a public repository, anyone can download the releases.

If the release step fails with a permission error, go to Settings → Actions → General →
Workflow permissions, select **Read and write permissions**, and run the workflow again.

## Install and set up

1. Open the APK on the phone and allow your browser or file manager to install unknown apps.
2. Open the app, then tap **Allow** next to **Notification access** and turn it on.
3. Tap **Allow** next to **Display over other apps** and turn it on.
4. If either switch is greyed out ("Restricted setting"): open App info → ⋮ → **Allow restricted settings**.
   The menu item may only appear after you have tried the greyed-out switch once.
5. Tap **Test bubble**.
6. If bubbles stop arriving after a while, set the app's battery usage to **Unrestricted** in App info.

**Updating:** each GitHub build is signed with a new temporary debug key, so uninstall the old
version before installing a new one. This clears your settings. A permanent signing key avoids this;
never commit that key to the repository.

## Gestures

| Gesture | Result |
|---|---|
| Tap | Opens the notification (or the app) and closes the bubble |
| Long press | Closes the bubble; the notification stays |
| Quick sideways flick | Closes the bubble; the notification stays |
| Slow drag | Moves the whole stack and saves the position |

## Behaviour

- Up to three bubbles, newest on top, with a `+N MORE` counter.
- A notification group shares one bubble. Updates don't create duplicates.
- No bubbles for ongoing notifications (music, downloads, calls in progress), minimised channels,
  notifications blocked by Do Not Disturb, or this app's own notifications.
- Only notifications that arrive while the app is connected get bubbles.
- Android hides overlays on the lock screen and some sensitive system screens.
- Dismissing the original notification removes its bubble.

## Privacy

The app has no internet permission and never reads notification titles or text.
It stores your settings and the package names (with last-seen times) of up to 30 recent apps.
The notification's open action is held in memory only. Backup is turned off.

## Build locally

Open the folder in Android Studio (JDK 17, Android SDK 36). From a terminal with Gradle 8.13:

    gradle testDebugUnitTest assembleDebug
