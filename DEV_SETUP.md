Local development setup (quick)
------------------------------

1) Required software
- Node.js (v18+), npm
- MongoDB (local or remote)
- Optional: `mkcert` if you want HTTPS for local testing (recommended for cookie Secure)

2) Example env files
- Backend: copy `backend/env.example` -> `backend/.env` and fill values (notably `MONGO_URI`, `ACCESS_TOKEN_SECRET`, `CLIENT_URL`).
- Frontend: copy `frontend/env.example` -> `frontend/.env` (Vite reads `VITE_` variables).

3) Run servers
- Backend:
  cd backend
  npm install
  npm run dev

- Frontend:
  cd frontend
  npm install
  npm run dev

4) Common issues & fixes
- CORS / cookies:
  - Make sure `CLIENT_URL` in backend/.env matches your frontend origin (e.g. http://localhost:5173).
  - For cross-origin cookies (refresh token) you need SameSite=None and Secure=true — Secure requires HTTPS. For local HTTP development the server defaults to Secure=false (development mode).

- HTTPS for cookies:
  - Install `mkcert` and add a local certificate for `localhost`.
  - Start frontend with HTTPS enabled (Vite supports `--https` with key/cert).
  - Set `NODE_ENV=production` only when you actually deploy; server behavior differs for secure cookies.

5) Troubleshooting
- If requests fail with CORS errors, check browser Console and Network → look at preflight response headers (`Access-Control-Allow-Origin`).
- If cookies are not set, ensure response `Set-Cookie` header present and browser is not blocking third-party cookies.

