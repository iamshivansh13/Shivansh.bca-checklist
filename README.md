# BCA Syllabus Checklist — Shivansh Maurya

An original, mobile-friendly BCA study checklist with topic completion tracking, progress bars, local auto-save, and optional Google sign-in / Cloud Firestore sync.

## Files
- `index.html` — page structure
- `style.css` — premium dark-blue responsive design
- `app.js` — syllabus data, checklist logic, local storage and optional Firebase sync

## Run locally
Because `app.js` uses JavaScript modules, run this folder through a local web server (for example VS Code Live Server), or publish it using GitHub Pages. Opening `index.html` directly as a `file://` URL may block module imports.

## Enable Google Login and cloud sync
1. Create a Firebase project at https://console.firebase.google.com/
2. Add a Web App and copy its Firebase configuration.
3. In Firebase Authentication, enable the Google provider.
4. In Authentication settings, add your deployed GitHub Pages domain to Authorized domains.
5. Create a Cloud Firestore database.
6. Replace the placeholder values in `firebaseConfig` near the top of `app.js`.
7. Publish the site over HTTPS.

### Starter Firestore rules
These rules let each signed-in user read and write only their own progress document in `studentProgress/{uid}`:

```text
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /studentProgress/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

Do not use open/public Firestore rules. Never put service-account private keys in frontend code. Firebase web config is designed to be included in a web app, but database access must be protected with Authentication and Security Rules.

## Important syllabus note
The included subject names and topic lists are starter/sample content to demonstrate the checklist. They are not represented as the official or complete RMLAU syllabus. Verify your current university syllabus and edit the `syllabus` object in `app.js` to match your course.

## Publish with GitHub Pages
1. Create a new GitHub repository, e.g. `shivansh-bca-checklist`.
2. Upload these three website files (`index.html`, `style.css`, `app.js`) and this README.
3. In repository Settings → Pages, choose deploy from the `main` branch and `/ (root)`.
4. Save and wait for GitHub Pages to publish your site.
