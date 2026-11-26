# Sparculator Troubleshooting & Diagnostics Cheatsheet

**Package Name:** `com.gigdriverapps.sparculator`

---

## 1. Live App & Crash Logs (`adb logcat`)

* **Stream only Python, Kivy, and fatal crash logs:**

  ```bash
  adb logcat -c && adb logcat -v time -s python:V PythonActivity:V AndroidRuntime:E
  ```

* **Stream logs filtered by Sparculator's exact running Process ID (PID):**

  ```bash
  adb logcat -c && adb logcat -v time --pid=$(adb shell pidof -s com.gigdriverapps.sparculator)
  ```

* **Dump the last 50 fatal crash / R8 / JNI lines:**

  ```bash
  adb logcat -d -v time | grep -iE "FATAL EXCEPTION|AndroidRuntime|ClassNotFoundException|Resources\$NotFoundException|Traceback|python" | tail -n 50
  ```

---

## 2. Google Play Store & Package Source Verification

* **Verify installed version, `versionCode`, and Play Store `packageSource=2`:**

  ```bash
  adb shell dumpsys package com.gigdriverapps.sparculator | grep -E "versionName|versionCode|packageSource|installerPackageName"
  ```

* **Clear stale Play Store cache when a new Internal Testing update gets stuck:**

  ```bash
  adb shell pm clear com.android.vending
  ```

* **Inspect Play Store (`Finsky`) and `PackageInstaller` errors during an update:**

  ```bash
  adb logcat -d -v time | grep -iE "PackageInstaller|Finsky|INSTALL_FAILED|status_code" | tail -n 30
  ```

* **Open your Internal Testing opt-in URL directly on your phone:**

  ```bash
  adb shell am start -a android.intent.action.VIEW -d "YOUR_INTERNAL_TEST_OPT_IN_URL"
  ```

---

## 3. Android Auto Service & Launcher Diagnostics

* **Force-stop Android Auto to reload launcher visibility and CarAppService bindings:**

  ```bash
  adb shell am force-stop com.google.android.projection.gearhead
  ```

* **Check `SparculatorCarAppService` binding and validator status:**

  ```bash
  adb shell dumpsys activity service com.google.android.projection.gearhead | grep -iE "sparculator|CarAppService"
  ```

* **Test Android Auto UI on Linux Desktop via Google's Desktop Head Unit (DHU):**

  ```bash
  adb forward tcp:5277 tcp:5277
  ~/.buildozer/android/platform/android-sdk/extras/google/auto/desktop-head-unit
  ```

---

## 4. Phone ↔ Auto State Sync & Foreground Timer Service

* **Inspect live synced calculation inputs and timer state (`auto_inputs.json`):**

  ```bash
  adb shell cat /sdcard/Android/data/com.gigdriverapps.sparculator/files/auto_inputs.json
  ```

* **List all files in Sparculator's external storage directory:**

  ```bash
  adb shell ls -la /sdcard/Android/data/com.gigdriverapps.sparculator/files/
  ```

* **Check if the background countdown service (`ServiceTimerservice`) is active:**

  ```bash
  adb shell dumpsys activity services com.gigdriverapps.sparculator
  ```

---

## 5. Build, R8 Mapping, & Play Console Release Pipeline

* **Auto-bump patch version, build signed `.aab` (`--no-install`), attach R8 `mapping.txt`, and publish to Internal Testing:**

  ```bash
  /devel/android/sparculator/tools/upload_play_internal.sh --build
  ```

* **Auto-bump minor or major version and publish:**

  ```bash
  /devel/android/sparculator/tools/upload_play_internal.sh --build minor
  /devel/android/sparculator/tools/upload_play_internal.sh --build major
  ```

* **Clear Gradle Configuration Cache if `build.gradle` hooks are modified:**

  ```bash
  rm -rf /devel/android/sparculator/.buildozer/android/platform/build-arm64-v8a/dists/sparculator/.gradle/configuration-cache
  ```

* **Reset cached `dists/sparculator` completely for a clean Gradle/AGP rebuild:**

  ```bash
  rm -rf /devel/android/sparculator/.buildozer/android/platform/build-arm64-v8a/dists/sparculator
  ```
