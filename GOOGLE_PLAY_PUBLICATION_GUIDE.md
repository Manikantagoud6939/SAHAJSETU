# SAHAJSETU — Google Play Store Publication Guide

This document provides the complete, step-by-step master roadmap for publishing **SAHAJSETU** (including **Local Shop AI**, **FarmLink Marketplace**, and **FoodShare Network**) as an official Android App on the **Google Play Store**.

---

## 🏗️ Architecture: Trusted Web Activity (TWA)

Google officially recommends **Trusted Web Activities (TWA)** for progressive web applications. With TWA:
- Your application runs as a **100% native Android app** installed from Google Play.
- It runs full-screen without any browser address bar (via Digital Asset Links verification).
- When you update your website/web app, updates reflect instantly inside the Android app without having to re-submit new builds to Google Play every time!

---

## 📋 Prerequisites

1. **Google Play Developer Account:**
   - Register at [play.google.com/console](https://play.google.com/console).
   - One-time registration fee: **$25 USD**.
   - Requires ID verification and D-U-N-S number (if registering as an organization) or personal verification.
2. **Domain Deployment:**
   - The app must be served over **HTTPS** (already configured on Vercel: `https://sahajsetu.vercel.app` or your custom domain).
3. **PWA Assets (Already prepared in this repository):**
   - ✅ `manifest.json` — PWA Web App Manifest
   - ✅ `sw.js` — Service Worker with offline caching
   - ✅ `icons/icon-192.png` & `icons/icon-512.png` — Standard & Maskable app icons
   - ✅ `privacy-policy.html` — Public privacy policy (strictly required by Google Play)
   - ✅ `terms-of-service.html` — Terms of service
   - ✅ `.well-known/assetlinks.json` — Digital Asset Links verification

---

## 🛠️ Step 1: Generate the Android App Bundle (`.aab`)

You have two simple options to generate the `.aab` file required by Google Play Console:

### Option A: Using PWABuilder (Easiest — 2 Minutes, No CLI Required)

1. Go to **[pwabuilder.com](https://www.pwabuilder.com/)**.
2. Enter your deployed URL: `https://sahajsetu.vercel.app` (or your custom domain) and click **Start**.
3. PWABuilder will audit your PWA (manifest, service worker, security — all will pass green).
4. Click **Package for Store** -> Choose **Android / Google Play**.
5. Configure package settings:
   - **Package ID:** `com.sahajsetu.app`
   - **App Name:** `SAHAJSETU`
   - **Launcher Name:** `SahajSetu`
   - **Version:** `1.0.0` (Version code: `1`)
   - **Display Mode:** `Standalone / Fullscreen`
6. Click **Generate** and download the `.zip` archive.
   - Inside the archive, you will find `app-release-bundle.aab` and your signing key.

---

### Option B: Using Google's Official Bubblewrap CLI (Advanced / CI/CD)

Google's Chrome team maintains `bubblewrap` to build TWAs:

```bash
# 1. Install Bubblewrap CLI globally
npm install -g @bubblewrap/cli

# 2. Initialize from your live manifest
bubblewrap init --manifest="https://sahajsetu.vercel.app/manifest.json"

# 3. Build the signed Android App Bundle (.aab)
bubblewrap build
```

This will output:
`app-release-bundle.aab` (upload this to Google Play Console).

---

## 🔑 Step 2: Configure Digital Asset Links (Removes URL bar)

For the app to open in immersive full-screen native mode without Chrome's URL bar:

1. When you generate your keystore, copy the **SHA-256 certificate fingerprint**.
   *(If using Google Play App Signing, copy the SHA-256 fingerprint from Play Console -> Setup -> App Signing).*
2. Open [`.well-known/assetlinks.json`](file:///C:/Users/manik/.gemini/antigravity/scratch/sahajsetu-website/.well-known/assetlinks.json):
   ```json
   [
     {
       "relation": ["delegate_permission/common.handle_all_urls"],
       "target": {
         "namespace": "android_app",
         "package_name": "com.sahajsetu.app",
         "sha256_cert_fingerprints": [
           "PASTE_YOUR_SHA256_FINGERPRINT_HERE"
         ]
       }
     }
   ]
   ```
3. Commit and push this file so it is reachable at:
   `https://<your-domain>/.well-known/assetlinks.json`

---

## 🎨 Step 3: Google Play Store Listing Dossier

Copy and paste these pre-crafted store listing details into Google Play Console:

### App Details
- **App Name (Max 30 chars):** `SAHAJSETU: Grassroots Commerce`
- **Short Description (Max 80 chars):** `Local Shop AI voice billing, direct FarmLink agri-trade & FoodShare rescue.`
- **Full Description:**
```text
SAHAJSETU connects neighborhood stores, farmers, and community institutions through an intelligent, vernacular digital ecosystem.

Flagship Pillars:

1. LOCAL SHOP AI
• Voice-Powered Billing: Speak naturally in Hindi, Tamil, Bengali, Marathi, or Hinglish to generate instant itemized bills in 3 seconds.
• Smart Inventory: Predictive stock replenishment alerts before high-demand staples run out.
• Automated Customer Khata: Digital WhatsApp invoicing and credit reconciliation.

2. FARMLINK MARKETPLACE
• Direct Farm-to-Retail Trade: Connect Farmer Producer Organizations (FPOs) directly with neighborhood shops and wholesale kitchens.
• Fair Realization: Eliminate 4-7 intermediate middlemen markups; growers earn 30-40% higher net realization.
• Transparent Pricing: Live APMC mandi price benchmarking and cold-chain route aggregation.

3. FOODSHARE NETWORK
• Zero-Waste Community Rescue: 1-tap surplus dispatch connecting supermarkets, caterers, and restaurants with registered shelters and food banks.
• Verified Food Safety: Rigorous hygiene guidelines and digital audit trails.
• ESG & Tax Benefits: Automated documentation for Section 80G tax benefits and carbon offset credits.

Empower your local community. Download SahajSetu today.
```

### Store Graphic Assets Required
- **App Icon:** 512 x 512 px PNG (32-bit with alpha) — *Available at `/icons/icon-512.png`*
- **Feature Graphic:** 1024 x 500 px JPEG or 24-bit PNG (no alpha)
- **Phone Screenshots:** At least 2 screenshots (minimum 320px, maximum 3840px; 16:9 or 9:16 aspect ratio).
- **Privacy Policy URL:** `https://<your-domain>/privacy-policy.html`

---

## 🚀 Step 4: Submission on Google Play Console

1. In Google Play Console, click **Create App**:
   - Name: `SAHAJSETU`
   - Default language: `English (India) - en-IN`
   - App or Game: `App`
   - Free or Paid: `Free`
2. Complete the **Set up your app** mandatory questionnaire:
   - **Privacy Policy:** Enter your deployed privacy policy URL.
   - **App Access:** All functionality is available without special credentials (or provide demo test login).
   - **Ads:** Select "No, my app does not contain ads".
   - **Content Rating:** Complete the IARC questionnaire (Utility / Business / Shopping).
   - **Target Audience:** 18 and older.
   - **Financial Features / Government Apps:** Select "Does not provide financial/government features" (unless licensed banking integrations are enabled).
   - **Data Safety:** Declare microphone access (only used dynamically during active voice billing sessions, ephemeral processing).
3. **Create Release:**
   - Go to **Testing -> Closed testing** (or Internal testing).
   - Upload your `app-release-bundle.aab`.
   - Add release notes: *"Initial launch of SAHAJSETU v1.0.0 — Empowering grassroots commerce, agriculture, and hunger relief."*
4. Click **Review & Rollout to Internal/Closed Testing**.
5. Once verified with your tester group, promote to **Production** track for Google's review team approval!
