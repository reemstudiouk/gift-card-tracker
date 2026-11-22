# Gift Card Wallet: setup

The app works straight away in **demo mode** (example cards, saved only on the device you use). These steps turn on sharing between you and your wife. They take about 15 minutes and cost nothing.

## 1. Create the Firebase project (sign-in and shared storage)

1. Go to https://console.firebase.google.com and sign in with your Google account.
2. Click **Create a project**, name it something like `gift-cards`. You can turn Google Analytics off.
3. In the left menu open **Build > Authentication**, click **Get started**, choose **Google**, switch it on, pick your email as the support email, and **Save**.
4. Open **Build > Firestore Database**, click **Create database**, choose a location near you (for the UK, `europe-west2 (London)`), and start in **production mode**.
5. In Firestore, open the **Rules** tab. Replace everything with the contents of `firestore.rules`, put your two Gmail addresses in place of the examples, and click **Publish**. Only those two accounts can then read or change the cards.
6. Open **Project settings** (gear icon) > **Your apps**, click the web icon `</>`, give it a name, and register it (no hosting needed). Firebase shows a `firebaseConfig` block. Copy its values into `config.js`, replacing the `PASTE_YOUR_API_KEY` placeholders.

## 2. Put the app online (GitHub Pages, free)

1. On GitHub, create a new repository, e.g. `gift-cards`.
2. Upload all the files from this folder: `index.html`, `config.js`, `manifest.webmanifest`, `icon.svg`, `icon-192.png`, `icon-512.png` (the rules and this file are optional).
3. In the repository open **Settings > Pages**, set **Source** to *Deploy from a branch*, branch `main`, folder `/ (root)`, and save. After a minute the app is at `https://<your-github-name>.github.io/gift-cards/`.
4. Back in Firebase: **Authentication > Settings > Authorized domains > Add domain**, and add `<your-github-name>.github.io`.

The code being public is fine: the Firebase settings in `config.js` aren't secret, and the rules from step 1.5 are what keep the cards private.

## 3. On both phones

1. Open the app's address and tap **Sign in with Google**, each with your own account.
2. Add it to the home screen. iPhone: Share button > *Add to Home Screen*. Android: Chrome menu > *Add to Home screen*.
3. Tap the gear icon once to set both names and the currency.

## Good to know

- Card screenshots are shrunk on your phone and saved in the same Firestore database, so you don't need Firebase Storage or a paid plan. Once a card has been opened on a phone, its screenshot also works without signal at the till.
- Card numbers and PINs are stored in your Firebase database, readable only by the two allowed accounts, and hidden in the app until you tap Show.
- To let another person in later, add their email to the rules and publish again.
