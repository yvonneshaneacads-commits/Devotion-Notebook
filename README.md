# Devotion Notebook

A cozy devotion journal that works in any browser and installs like an app. Your notes sync between phone and laptop through your own free Firebase account.

## Put it online with GitHub Pages
1. Create a GitHub repository and upload everything in this folder (index.html, sw.js, manifest.webmanifest and the icon files).
2. In the repository go to **Settings > Pages**, choose **Deploy from a branch**, pick `main` and `/ (root)`, and save.
3. After a minute your notebook is live at `https://YOUR-USERNAME.github.io/REPO-NAME/`.

## Turn on sign-in and sync (Firebase, free plan is enough)
1. Go to https://console.firebase.google.com and **Add project**.
2. In the project, click the web icon (`</>`) to **register a web app**. Copy the config it shows (apiKey, authDomain, projectId, appId).
3. **Build > Authentication > Get started > Sign-in method**: turn on **Google**.
4. **Authentication > Settings > Authorized domains**: add `YOUR-USERNAME.github.io`.
5. **Build > Firestore Database > Create database**, then open the **Rules** tab and paste this, then **Publish**:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

6. Connect the notebook. Pick one:
   - Open your live site, tap **Settings**, paste the config into the Firebase box, then **Sign in with Google**. Repeat the paste on each device.
   - Or open `index.html`, find `var FIREBASE_CONFIG=null;` and replace `null` with your config, like `{apiKey:"...",authDomain:"...",projectId:"...",appId:"..."}`. Commit it. Every device then only needs to sign in. The web config is not a secret; the rules above are what keep your notes private.

If this device already has notes and your account has notes too, the account version wins. Download a backup in Settings first if unsure.

## Install it like an app
- **iPhone/iPad (Safari):** Share > **Add to Home Screen**.
- **Android (Chrome):** menu > **Install app**.
- **Laptop (Chrome/Edge):** the install icon in the address bar.

## Music
Settings has a music box for YouTube or Spotify links. Spotify plays full songs only if you are signed in to Spotify in the same browser.
