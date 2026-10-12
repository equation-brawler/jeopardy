# Jeopardy Builder

Build Jeopardy boards with fonts, images, LaTeX and code blocks, save them as public or password-locked private boards, and play them with team scoring. No accounts: everything runs in the browser, and boards are stored in Cloud Firestore.

Live: https://jeopardy-builder.github.io/

## How saving works

- Every board is gzipped and stored as base64 chunks under `boards/{id}/c/`.
- Private boards are encrypted in the browser with AES-GCM using a key derived from the password (PBKDF2-SHA-256, 200k iterations). The database never sees the title, the content or the password.
- A board opens with its title + password. Public boards are also listed for anyone to play.
- Changing or deleting a board requires a password-derived proof checked by `firestore.rules`.

## Setup

1. Create a Firebase project and add a **Web app**; copy its config into `window.FIREBASE_CONFIG` in `index.html`.
2. Create a **Cloud Firestore** database (production mode).
3. Paste `firestore.rules` into Firestore → Rules and publish.
4. Serve `index.html` from any static host (GitHub Pages serves this repo's `main` branch).

The Firebase web config is public by design; the rules are what protect the data.
