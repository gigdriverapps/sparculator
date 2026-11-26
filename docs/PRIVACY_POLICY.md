# Privacy Policy for Sparculator

**Effective Date:** November 25, 2026  
**Developer:** gigDriverApps  
**Package Name:** `com.gigdriverapps.sparculator`

## 1. Overview

Sparculator ("the App") is a delivery wait-time and hourly-rate calculator designed for independent gig delivery drivers. Your privacy is important to us. **Sparculator does not collect, transmit, sell, or share any personal or device data with external servers or third parties.**

## 2. Data Stored Locally on Your Device

To provide core functionality—including syncing your active countdown timer and rate inputs between your phone and Android Auto—the App saves configuration and session state locally on your device's internal/app-scoped storage:

* **Calculation Inputs:** Offer pay, target hourly rate, estimated trip duration, wait pay rate, and grace period settings.
* **Timer State:** Active timer start time, target end timestamp, and remaining duration so your countdown continues reliably in the background and on your car display.

All stored data remains strictly on your device and is automatically deleted if you clear the App's storage or uninstall the App.

## 3. Permissions Used

Sparculator requests only the minimum Android permissions required for timer notifications:

* **Notifications (`POST_NOTIFICATIONS`) & Full-Screen Intent (`USE_FULL_SCREEN_INTENT`):** Used to display your active wait-time countdown and expiration alert on your phone and Android Auto screen.
* **Vibration (`VIBRATE`) & Wake Lock (`WAKE_LOCK`):** Used to trigger tactile vibration alerts when your walk-away deadline expires while the screen is off.
* **Foreground Service (`FOREGROUND_SERVICE` / `FOREGROUND_SERVICE_SPECIAL_USE`):** Keeps your user-initiated wait timer accurate when switching apps or driving.

## 4. Third-Party Services & Analytics

Sparculator contains **no** third-party advertising SDKs, **no** behavioral analytics or crash-tracking trackers, and **no** cloud accounts.

## 5. Children's Privacy

Sparculator is intended for adult gig-economy drivers and is not directed to children under the age of 13.

## 6. Changes to This Policy

We may update this Privacy Policy from time to time. Any updates will be posted at this URL with a revised effective date.

## 7. Contact Us

If you have any questions about this Privacy Policy, you may contact the developer at:  
**Email:** <gigdriverapps@bstivers.dev>
