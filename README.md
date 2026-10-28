# AppSprouts — Privacy Policy & Account Deletion Portal

This repository hosts the official Privacy Policy and Account Deletion portal for **AppSprouts**, ready for one-click deployment on [Vercel](https://vercel.com).

## Key Features

- **Compliant Account Deletion**: Fully reflects the **90-day deletion timeline** for Google Play & App Store developer policy compliance.
- **Vercel Ready**: Preconfigured with `index.html` and `vercel.json` for zero-configuration static deployment.
- **Direct Google Sheet Logging**: Includes asynchronous request submission directly into a Google Sheet via a lightweight Google Apps Script Web App.
- **Fallback Redundancy**: If the direct endpoint is unavailable or unconfigured, the form gracefully falls back to opening the user's default email client with a pre-formatted 90-day deletion request.

---

## 🚀 Google Sheet Logging (Connected)

This portal is connected to your Google Apps Script Web App:
- **Endpoint**: `https://script.google.com/macros/s/AKfycbw9iapxA276ecH85sQ8BWeKBg1WPcYmWvDd8fJInw3zn_C7pQATGtRfvg89Tj9hxPUAxw/exec`
- Whenever a user enters their email and submits the deletion form, it appends a row with:
  - `timestamp`: ISO timestamp
  - `email`: User's account email
  - `targetPurgeDate`: Exact date 90 days from the request
  - `policy`: "90-Day Deletion"
- Tested and verified: Rows append in real-time.

---

## 🌐 Deploying to Vercel

1. Log in to [Vercel](https://vercel.com).
2. Click **Add New...** > **Project**.
3. Select this repository from your GitHub list (`Theguyjazzy/appsprouts-privacy`).
4. Click **Deploy** (no build settings or environment variables required).
5. Done! Your privacy policy is live with automatic SSL.
