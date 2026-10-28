# AppSprouts — Privacy Policy & Account Deletion Portal

This repository hosts the official Privacy Policy and Account Deletion portal for **AppSprouts**, ready for one-click deployment on [Vercel](https://vercel.com).

## Key Features

- **Compliant Account Deletion**: Fully reflects the **90-day deletion timeline** for Google Play & App Store developer policy compliance.
- **Vercel Ready**: Preconfigured with `index.html` and `vercel.json` for zero-configuration static deployment.
- **Direct Google Sheet Logging**: Includes asynchronous request submission directly into a Google Sheet via a lightweight Google Apps Script Web App.
- **Fallback Redundancy**: If the direct endpoint is unavailable or unconfigured, the form gracefully falls back to opening the user's default email client with a pre-formatted 90-day deletion request.

---

## 🚀 One-Minute Google Sheet Setup (To Collect Deletion Requests)

A standard Google Sheet link cannot directly receive POST requests from the browser without an endpoint. The simplest, 100% free way to log requests is using Google Apps Script:

1. Open your Google Sheet (e.g. named `AppSprouts Account Deletion Requests`).
2. Give Row 1 the headers:
   - **Column A**: `Timestamp`
   - **Column B**: `Email`
   - **Column C**: `Target Purge Date (90 Days)`
   - **Column D**: `Policy`
3. In the top menu, go to **Extensions > Apps Script**.
4. Replace any existing code in the editor with:
   ```javascript
   function doPost(e) {
     var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
     var data = JSON.parse(e.postData.contents);
     sheet.appendRow([
       data.timestamp || new Date().toISOString(),
       data.email,
       data.targetPurgeDate,
       data.policy || "90-Day Deletion"
     ]);
     return ContentService.createTextOutput(JSON.stringify({ result: "success" }))
       .setMimeType(ContentService.MimeType.JSON);
   }
   ```
5. Click **Deploy** (blue button in top-right) > **New deployment**.
6. Under *Select type*, pick **Web app**.
   - **Description**: `AppSprouts Deletion Collector`
   - **Execute as**: `Me`
   - **Who has access**: `Anyone` *(Crucial so the form can submit without requiring Google sign-in)*
7. Click **Deploy** and copy the **Web app URL** (starts with `https://script.google.com/macros/s/.../exec`).
8. Paste that URL into line 282 of `index.html`:
   ```javascript
   const GOOGLE_SHEET_ENDPOINT = "https://script.google.com/macros/s/.../exec";
   ```
9. Commit and push to Git — Vercel will redeploy automatically!

---

## 🌐 Deploying to Vercel

1. Log in to [Vercel](https://vercel.com).
2. Click **Add New...** > **Project**.
3. Select this repository from your GitHub list (`Theguyjazzy/appsprouts-privacy`).
4. Click **Deploy** (no build settings or environment variables required).
5. Done! Your privacy policy is live with automatic SSL.
