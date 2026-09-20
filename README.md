# Personal Document Vault — REAL PWA Integration Test

This build uses the real Document Vault frontend structure, but runs it as an external GitHub Pages PWA.

Architecture:
GitHub Pages → Google OAuth → Apps Script API (`scripts.run`) → STAGING

There is NO iframe and NO Apps Script `/exec` UI.

The existing application JavaScript is preserved and a compatibility adapter implements `google.script.run` over the Apps Script API. The login function first obtains the Google OAuth token, then uses the existing `validateUser()` / `createAppSession()` flow.

## First test

1. Replace the GitHub Pages PWA files with the files in this folder.
2. Commit and push.
3. Open the GitHub Pages URL.
4. The normal Document Vault login page should appear.
5. Click **Sign in with Google**.
6. Complete Google authorization if prompted.
7. Expected: the normal authenticated Document Vault shell appears and the dashboard loads.

This build uses the existing STAGING API deployment with `devMode: true`.
Do not change production.

## Scope of this gate

This is the first real-shell go/no-go test. It deliberately does not attempt a full rewrite of every feature. The objective is to prove that the existing application UI can operate externally through the API adapter.
