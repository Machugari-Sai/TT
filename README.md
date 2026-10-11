# SAK Universe

SAK Universe is a responsive, login-first comics, books, and superhero story site. It uses plain HTML/CSS/browser JavaScript and a dependency-free Node.js backend.

## Structure

```text
Frontend/public/       UI pages, browser scripts, styles, artwork, comic archives
Backend/src/main/      Node server and API handling
Backend/src/test/      Backend test location (the current project uses syntax checks)
Frontend/src/           Frontend extension points for components, routes, and services
Backend/               Auth, persistence, package configuration, checks
Backend/data/          Local JSON data (users and sessions are runtime-generated)
docs/                  Architecture notes
```

## Requirements

- Node.js 18 or newer
- No `npm install` is required; the project uses Node built-ins only.

## Run the complete application

From the repository root:

```powershell
npm start
```

Open `http://127.0.0.1:8010/`. Unauthenticated HTML requests redirect to `auth.html`; successful login or registration opens `index.html`.

## Run the backend independently

```powershell
cd Backend
npm start
```

Set `PORT`, `HOST`, and `NODE_ENV` in the process environment. See `Backend/.env.example`. The server serves `Frontend/public/`.

## Check the project

```powershell
npm test
npm run check:frontend
```

There is no frontend production build because the UI is served as static files. `npm test` runs Node syntax checks for the backend and browser scripts.

## Authentication and persistence

The backend verifies password hashes, stores an HttpOnly session cookie, protects HTML routes and private APIs, and checks the admin role for the dashboard endpoint. Local JSON persistence lives in `Backend/data/`. Keep that directory on persistent storage in deployment, or migrate to a database for multi-instance production use.

## Deployment

For the complete application, use a Node 18+ service with start command `npm start`, configure `HOST=0.0.0.0` when required by the platform, enable `NODE_ENV=production`, and serve through HTTPS.

The static frontend can be deployed to Vercel from the repository root. The checked-in [`vercel.json`](vercel.json) sets `Frontend/public` as Vercel's output directory, which includes the `index.html` entry point and all static assets. Vercel will not provide the stateful Node backend or durable JSON persistence; deploy that backend separately and configure the frontend/API cookie architecture for the chosen domains before relying on login or other `/api/*` features.

See [docs/deployment.md](docs/deployment.md) for the recommended production architecture and the limitations of deploying the current stateful backend directly alongside a Vercel static frontend.
