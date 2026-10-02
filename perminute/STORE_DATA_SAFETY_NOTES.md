# Per Minute Content Reader — Store Privacy / Data Declaration Preparation Notes

> **Developer preparation notes — verify against current App Store Connect / Google Play declarations before submission.**
>
> *Notice: This document provides internal technical preparation notes based strictly on the current application architecture and repository evidence. It is not an official submission and does not constitute formal legal counsel. Verify all declarations in App Store Connect and Google Play Console prior to release.*

---

## 1. Application & Architectural Overview

- **Consumer App Name:** Per Minute Content Reader
- **Short Brand:** Per Minute
- **Technical Bundle / Package ID:** `com.readrush.readrush`
- **Supported Platforms:** iOS, Android
- **Core Architecture:** Account-free, offline-first, local sandbox storage
- **Backend / Cloud Services:** None. No proprietary application backend, no cloud database, no cloud AI inference endpoints, no remote reading history server, no remote document storage.
- **Advertising:** None in current release. No Google AdMob, no advertising SDKs, no ad consent CMP, no advertising ID usage.
- **Analytics / Telemetry:** None in current release. No Firebase Analytics, no Mixpanel, no Segment, no crash reporting SDK.

---

## 2. Apple Privacy Nutrition Label Analysis (App Store Connect)

Under Apple's App Store privacy questions, developers declare data collected by the app or third-party partners embedded in the app.

### A. Data Collection Summary (Apple)

| Data Category | Stored Locally on Device? | Collected Off-Device (Transmitted to Developer or Third Party)? | Linked to User Identity? | Used for Tracking (across apps/websites)? |
| :--- | :---: | :---: | :---: | :---: |
| **Contact Info** (Name, Email, Phone, Address) | **No** | **No** | No | No |
| **User Content** (Imported PDFs, EPUBs, TXTs) | **Yes** (in app local sandbox) | **No** (never transmitted to developer servers) | No | No |
| **Identifiers** (User ID, Device ID) | **No** | **No** (no proprietary account or device IDs generated) | No | No |
| **Usage Data** (Reading progress, WPM metrics, training results) | **Yes** (in local database / preferences) | **No** (stays on physical device) | No | No |
| **Purchases / Financial Info** | **No** (app only receives cryptographically signed local receipt / entitlement token from StoreKit) | **Handled by Apple** (Apple processes purchase according to Apple's Privacy Policy) | Not linked by developer (developer receives no card / billing data) | No |
| **Diagnostics / Crash Data** | **No** (standard OS-level crash reporting via Apple TestFlight/App Store diagnostics if user opted in at OS level) | **No developer SDK** | No | No |
| **Location Data** | **No** | **No** | No | No |

### B. Apple App Tracking Transparency (ATT)
- **Tracking:** **No**.
- The app does not track users across apps and websites owned by other companies.
- `AppTrackingTransparency.framework` is **not used**.
- No `NSUserTrackingUsageDescription` required.

---

## 3. Google Play Data Safety Section Preparation (Google Play Console)

Google Play requires developers to declare whether data is collected, shared, and how it is handled.

### A. Core Questions & Recommended Technical Answers

1. **Does your app collect or share any of the required user data types?**
   - **User Documents / Content:**
     - Data is stored *locally on device only*.
     - Under Google Play guidance, data processed ephemerally or stored only on-device without transmission to an external server does not count as "collected" or "shared".
   - **Financial Info / In-App Purchases:**
     - In-app purchases are executed through **Google Play Billing**.
     - Purchases are processed directly by Google. The app receives purchase tokens/entitlements to grant access. The app developer does not collect or store credit card numbers, bank accounts, or financial profiles.
2. **Is all of the user data collected by your app encrypted in transit?**
   - Since the app does not transmit user documents or reading data to developer servers, transit encryption applies only to platform-level billing communications handled by Google Play Billing and Apple StoreKit (which enforce TLS/HTTPS).
3. **Do you provide a way for users to request that their data be deleted?**
   - **Yes, via local in-app controls:** Users can delete imported documents and clear application data directly inside the app, or by uninstalling the application from their device. Because there is no developer server or cloud account, no remote deletion request is necessary.

---

## 4. Third-Party SDK & Dependency Audit

| Service / SDK | Type | Data Transmitted Off-Device | Purpose |
| :--- | :--- | :--- | :--- |
| **Apple StoreKit** (iOS) | Platform In-App Purchase | Apple receives purchase transactions; developer receives receipt/entitlement | Subscriptions & Lifetime unlock |
| **Google Play Billing** (Android) | Platform In-App Purchase | Google receives purchase transactions; developer receives purchase token | Subscriptions & Lifetime unlock |
| **Local Inference Model** | On-Device Intelligence | **None** (all computation executes on local processor) | Optional reading assistance |
| **Google AdMob / Ads** | None | **Not present in release** | N/A |
| **Firebase / Analytics** | None | **Not present in release** | N/A |
| **Crashlytics / Sentry** | None | **Not present in release** | N/A |

---

## 5. Technical Package & Store Configuration Reference

- **Consumer-Facing Title:** Per Minute Content Reader
- **Short Brand:** Per Minute
- **Technical Package ID:** `com.readrush.readrush`
- **In-App Products:**
  - `perminute.premium.monthly` (Monthly auto-renewable subscription)
  - `perminute.premium.annual` (Annual auto-renewable subscription, *Best Value*)
  - `perminute.premium.lifetime` (Lifetime one-time non-consumable)
- **Local In-App Trial:** 7 calendar days, local entitlement logic, triggers strictly on first RSVP or Training Sprint activation. Not a store introductory subscription offer.
- **Published Legal URLs:**
  - **Privacy Policy:** `https://arunnagelly.github.io/perminute/privacy.html` (and root alias `https://arunnagelly.github.io/perminuteprivacypolicy.html`)
  - **Terms of Use:** `https://arunnagelly.github.io/perminute/terms.html`
  - **Support:** `https://arunnagelly.github.io/perminute/support.html`
- **Support Contact:** `nagellyarunkumar@gmail.com`
