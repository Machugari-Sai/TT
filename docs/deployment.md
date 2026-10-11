# Deployment guide

## Recommended production deployment

Deploy the complete repository as one Node.js service. The backend serves `Frontend/public/` and the same-origin API routes, which is required for the current HttpOnly session-cookie design.

1. Use Node.js 18 or newer.
2. Set the service start command to `npm start`.
3. Set `HOST=0.0.0.0`, provide the platform `PORT`, and set `NODE_ENV=production`.
4. Enable HTTPS so the production session cookie is secure.
5. Mount persistent storage for `Backend/data/`, or migrate users, sessions, reviews, and ratings to a production database.
6. Verify `/`, `/auth.html`, `/api/profile`, and `/logout` after deployment.

## Vercel compatibility

The current application is not a complete single-project Vercel deployment. Vercel can serve the static files in `Frontend/public/`, but the stateful Node server and local JSON persistence should not be treated as durable Vercel serverless storage. The frontend also currently calls same-origin `/api/*` routes and relies on same-origin HttpOnly cookies.

For a Vercel frontend plus separately hosted backend, the API client must be changed to use a configured backend origin, the backend must configure an explicit production CORS origin, and cookie settings must be designed for the chosen domains. Those values cannot be safely invented without the real frontend URL, backend URL, and database/storage choice.

Do not claim a Vercel deployment until the frontend, backend, persistent storage, environment variables, cookies, CORS, and protected-route flow have been verified together.

## GitHub readiness

The repository has a root `.gitignore`, safe `.env.example` files, and no detected common credential patterns. This workspace does not contain a usable `.git` worktree, so no commit, branch, history inspection, or push was performed.
