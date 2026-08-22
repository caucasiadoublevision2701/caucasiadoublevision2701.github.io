# Counter Room Sample Register — Firebase edition

This version runs as a static website and no longer uses Google Apps Script or Google Sheets.
Records are stored in Firebase Realtime Database. Users sign in anonymously in the background.

## Configure Firebase

1. Create a project in the Firebase Console.
2. Add a Web app and copy its configuration object.
3. In `index.html`, replace every `PASTE_...` value inside `firebaseConfig`.
4. Open **Build > Authentication > Sign-in method** and enable **Anonymous**.
5. Open **Build > Realtime Database**, create a database, and choose the region you want.
6. Install the Firebase CLI and sign in:

   ```bash
   npm install -g firebase-tools
   firebase login
   ```

7. From this folder, connect the project and deploy the database rules and Hosting:

   ```bash
   firebase use --add
   firebase deploy --only database,hosting
   ```

## Publish the same source on GitHub

Create a GitHub repository and push this folder. Keep `firebase.json`, `database.rules.json`,
`README.md`, and `index.html` in the repository. Firebase web configuration is designed to be
present in client code; access control belongs in Firebase rules.

If you use GitHub Pages instead of Firebase Hosting, publish `index.html` from the repository root.
The Firebase database and anonymous authentication continue to work as the backend.

## Important

The app still stores compressed photos as base64 strings in Realtime Database to preserve the
existing behavior. For a larger production deployment, migrate photos to Firebase Storage and
store only their URLs in the database.
