# CAT Coach (PWA starter)

A local-first, installable Progressive Web App for CAT preparation tracking.

## Features
- Daily adaptive targets based on recent accuracy and recorded error counts.
- Practice, sectional and mock performance logging.
- Error bank with category, diagnosis, answers and optional screenshot attachments.
- Topic revision schedule using 1/3/7/14-day intervals; incorrect retrieval resets to next-day review.
- Surprise revision question selected from seeded examples and previously recorded errors.
- JSON backup and restore.
- Browser notifications while the app is open; service worker caches the app for offline use.

## Run locally
Service workers and install prompts require localhost or HTTPS. From this directory run:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000` in a browser.

## Install on Android
1. Host the folder on an HTTPS static host (for example, a static site host).
2. Open the HTTPS URL in Chrome on Android.
3. Use Chrome menu → **Install app** or **Add to Home screen**.
4. Open CAT Coach and enable notifications.

## Important limitations of this starter
- Data is stored in the browser's localStorage on this device. It does not sync across devices. Export JSON backups regularly.
- Screenshot files are encoded into the local browser database payload. Large or numerous screenshots can exceed browser storage limits.
- The starter can schedule surprise alerts only while the app's JavaScript is running. It cannot reliably send random push notifications while fully closed.
- Reliable closed-app push requires HTTPS, a push subscription, a VAPID key pair, and a backend scheduler (for example, a small Node service plus a database). This is not included or configured.
- Screenshot attachments are stored but not OCR-parsed. You can inspect them and manually enter results; automated screenshot extraction requires an OCR/vision service.
- Seed question bank is illustrative and small. Replace/expand it with licensed or user-provided practice questions. Do not upload copyrighted coaching PDFs for redistribution.

## Suggested production architecture
- PWA frontend: this project.
- Auth + database: Supabase (Postgres) or Firebase.
- Storage: private object storage for screenshots.
- Push: Web Push API + VAPID + server-side scheduled jobs.
- AI analysis: explicit user-triggered screenshot/question analysis, with extracted scores confirmed before saving.

## Data model (production)
`users`, `study_sessions`, `mock_attempts`, `section_scores`, `errors`, `topics`, `revision_events`, `question_bank`, `push_subscriptions`, `attachments`.
