# Shobhit Web

Responsive learning website with learning roadmap, project ideas, signup/login pages, dashboard, and an Express API.

## Run locally

Requires Node.js 20+.

```bash
npm install
cp .env.example .env
```

Set a long random `SESSION_SECRET` in `.env`, then run `npm run dev` and open http://localhost:3000. Health check: http://localhost:3000/api/health.

## Deployment and security

- Signup, login, sessions, and API routes need a Node.js host; GitHub Pages cannot run `server.js`.
- Set `NODE_ENV=production` and a strong `SESSION_SECRET` on the server, use HTTPS, and never commit `.env` or `data/`.
- The JSON user file is a demo store, not production-grade database storage. Use a persistent database and backups for a public launch.
- Contact form currently validates input only; it does not email or save messages.
- For production, review session cookie, proxy, CORS, and CSRF settings for your chosen host.

## Automatic Android APK

Capacitor wraps the `public/` folder into an Android app. The APK does not run the Express server itself, so signup/login/contact API calls need a deployed backend.

1. Deploy the Node.js backend to an HTTPS host.
2. Set `window.SHOBHIT_API_BASE` in `public/config.js` to that backend URL. Configure CORS and session cookie policy for the app's WebView origin before using authentication.
3. Push the project to GitHub and open **Actions → Build Android APK**. The workflow creates the Android project, builds a debug APK, and uploads it as the `shobhit-web-debug-apk` artifact.
4. Open the successful workflow run and download its artifact.

The workflow produces a debug APK for testing, not a signed Google Play release. Release distribution requires signing and proper key management.
