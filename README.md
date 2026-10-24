# CGPSC Test Series Planner — Cloud Login Edition

This package turns the original single-file planner into a hosted website with:
- Email/password login and account creation
- Per-user cloud storage for task checks, test marks, weak topics, and notes
- Browser-local backup plus Firestore cloud sync
- Password reset by email
- CSV export
- Firestore rules that restrict each account to its own record

## Important
You must create/configure your own Firebase project before publishing. This package does not include or invent project credentials. Never share your Firebase password or any private service-account key.

## Setup (one-time, around 10–15 minutes)

1. Open https://console.firebase.google.com/ and create a Firebase project.
2. In Project settings → General → Your apps, add a Web app and copy its Firebase config.
3. In Firebase Authentication → Sign-in method, enable **Email/Password**.
4. In Firestore Database, create a database (production mode is fine).
5. The Firebase web configuration you supplied is already inserted into `index.html`. Verify it matches your project in Project settings → General → Your apps. Firebase web config is public client configuration, not a service-account secret.
6. Install Node.js if it is not already installed, then install Firebase CLI:
   ```bash
   npm install -g firebase-tools
   ```
7. In a terminal, open this folder and run:
   ```bash
   firebase login
   firebase use --add
   firebase deploy
   ```
   Select the project you created. The CLI will publish the site and apply the included Firestore rules.
8. Open the Hosting URL printed by Firebase. Create an account using your email and a strong password.

## Deploy from the Firebase Console / GitHub
You can also upload the files to a GitHub repository and use Firebase Hosting's GitHub integration, but the Firebase CLI is the simplest path.

## Data and security notes
- Passwords are managed by Firebase Authentication; this app does not write passwords into Firestore.
- The planner saves one document at `users/{your-auth-uid}`. Firestore rules allow a user to access only their own document.
- Keep the Firebase project owner account secure and enable two-factor authentication on your Google account.
- The site uses Firebase SDKs from Google's CDN, so it needs an internet connection.
- Cloud sync requires the Firebase config to be filled in and the Firestore rules to be deployed.
- If you had progress in the original local-only planner, the cloud version attempts to migrate that browser's saved state on your first sign-in **when that same browser still has the old local storage entry**.
- Test the app with a second account to verify accounts cannot see each other's records.
