# voter.gg — GitHub Pages + Firebase setup

GitHub Pages hosts the static website. Firebase provides shared accounts and live poll data.

## 1. Create Firebase project

1. Go to https://console.firebase.google.com/ and create a project.
2. Add a **Web app** and copy its web configuration.
3. In **Authentication → Sign-in method**, enable **Email/Password**.
4. In **Firestore Database**, create a database.

## 2. Add the Firebase config

Open `voter-gg.html` and find the `firebaseConfig` object near the bottom. Replace the placeholder values with the matching `apiKey`, `authDomain`, `projectId`, and `appId` from your Firebase web app config. Keep the property names unchanged.

The Firebase web API key is expected to be present in client-side web apps. Database access is controlled by the Firestore rules below.

## 3. Publish Firestore rules

In Firebase Console → **Firestore Database → Rules**, replace the rules with the contents of `firestore.rules` and click **Publish**.

The rules allow visitors to read polls and public profile details, but require authentication to create polls, vote, comment, or edit one's own profile. Passwords are handled by Firebase Authentication and are not stored in Firestore.

## 4. Publish on GitHub Pages

Upload these files to the root of your GitHub Pages repository:

- `index.html` (rename `voter-gg.html` to this if you want the website root to open directly)
- `everybody-votes-logo.png`
- `firestore.rules` (reference copy; Firebase does not deploy it automatically)
- `SETUP.md` (optional reference)

In GitHub → **Settings → Pages**, select your deployment branch and `/ (root)` folder.

## Notes

- Users enter a username and password. Internally, usernames map to Firebase email-style IDs (`username@voter.gg`).
- Old accounts in the previous Claude-only database do not migrate automatically; users will need to create accounts again.
- Polls, profile names/photos, votes, and comments are public to visitors. Users should not reuse passwords from other services.
- Configure Firebase usage alerts and review its billing limits before sharing the site widely.
