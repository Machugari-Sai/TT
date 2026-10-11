# Architecture

SAK Universe is a dependency-free multi-page frontend served by a small Node.js backend.

- `Frontend/public/` contains HTML pages, shared CSS, browser JavaScript, artwork, comic folders, and public metadata.
- `Backend/src/main/server.js` serves `Frontend/public/`, enforces the login-first HTML boundary, and owns the JSON APIs.
- `Backend/data/` contains local persistence for users, sessions, reviews, and comic ratings. Runtime account/session files are ignored by Git.
- The root `package.json` delegates to the independent frontend and backend package scripts.

There is no bundler, database driver, or runtime dependency. Production deployments should mount persistent storage for `Backend/data/` or replace the JSON store with a transactional database.
