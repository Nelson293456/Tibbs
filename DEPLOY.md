# Deploying Mr Tibbs — Crossy Cat

Ten minutes, all free tier. You need Node.js installed.

## 1. One-time setup

```
npm install -g firebase-tools
firebase login
```

Put these three files in one folder: `index.html`, `firebase.json`, `firestore.rules`.

## 2. Connect to your project

In that folder:

```
firebase use --add
```

Pick your existing project (tibs-37fc2).

## 3. Deploy

```
firebase deploy
```

That pushes the game to hosting AND applies the Firestore rules (which now
include the daily leaderboards) in one command. It prints your live URL,
something like `https://tibs-37fc2.web.app`.

## 4. Authorize the domain for sign-in

Firebase Console -> Authentication -> Settings -> Authorized domains.
`tibs-37fc2.web.app` is usually pre-authorized; if you use a custom domain,
add it here or Google sign-in will refuse.

Also confirm under Authentication -> Sign-in method that **Anonymous** and
**Google** are both enabled.

## 5. Updating the game later

Replace `index.html` in the folder and run `firebase deploy` again. Done.

## Troubleshooting

- Leaderboard says "offline" with a file:// message -> you opened the HTML
  from disk. It must be served over http(s). For quick local testing:
  `python3 -m http.server` then visit http://localhost:8000
- Sign-in fails with `auth/unauthorized-domain` -> step 4.
- Daily board empty -> it's per-UTC-day; scores appear once someone
  finishes a daily run today.
