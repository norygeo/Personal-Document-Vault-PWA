# Personal Document Vault — External PWA POC

## Purpose

This is a STAGING-only proof of concept for testing an external PWA shell
around the existing Google Apps Script Personal Document Vault.

The shell owns:
- the real web manifest
- the 192x192 icon
- the 512x512 icon
- the outer PWA document

The existing GAS application remains inside the iframe.

## Important security boundary

This POC must point ONLY to the STAGING Apps Script Web App `/exec` URL.

Do NOT put:
- production URLs
- passwords
- tokens
- Drive IDs
- spreadsheet IDs
- document data
- other secrets

into this repository.

## Before publishing

Open `index.html` in VS Code and replace:

    YOUR_STAGING_GAS_EXEC_URL

with the deployed STAGING Web App `/exec` URL.

Example:

    https://script.google.com/macros/s/YOUR_STAGING_ID/exec

Do not add `?asset=manifest` to the iframe URL.

## Local folder

Keep this project separate from the Apps Script/clasp project.

Recommended structure:

    DocVault-External-PWA-POC/
    ├── index.html
    ├── manifest.webmanifest
    ├── icon-192.png
    ├── icon-512.png
    └── README.md

## Git / GitHub workflow

From the VS Code terminal:

    git init
    git add .
    git commit -m "Initial external PWA POC"
    git branch -M main
    git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
    git push -u origin main

Then enable GitHub Pages for:
- Branch: `main`
- Folder: `/ (root)`

## POC tests

1. Open the GitHub Pages HTTPS URL.
2. Confirm the PWA shell loads.
3. Confirm Chrome DevTools → Application → Manifest detects:
   - Personal Document Vault
   - Doc Vault
   - standalone
   - 192x192 icon
   - 512x512 icon
4. Confirm the GAS vault renders inside the iframe.
5. Test normal navigation/session behavior.
6. Test a safe read-only document operation.
7. Test upload/download only if needed after the initial rendering test.
8. Compare launch/perceived performance with the direct STAGING GAS URL.

## No service worker yet

This POC intentionally has no service worker. We are first testing:
- manifest recognition
- icon recognition
- rendering
- iframe behavior
- functional compatibility
- performance

If this architecture proves viable, service-worker design will be considered separately.

## Source of truth

All code changes should be made in VS Code and pushed to GitHub.
Do not edit the repository files through the GitHub web editor for this POC.
