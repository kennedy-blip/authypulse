# AuthPulse

JWT Inspector, OAuth2/OIDC token debugging workspace, session ledger, and RBAC policy sandbox.

## Stack
- Vite + React + TypeScript
- Tailwind CSS v4 via `@tailwindcss/vite`
- Vercel Serverless Functions (`/api`)
- RS256 demo JWT issuer using Node's built-in crypto

## Local development
```bash
npm install
npm run dev
```
The Vite dev server proxies `/api` to `http://localhost:3000`. Run `vercel dev` for the complete frontend + serverless experience. If the API is unavailable, the UI provides a clearly labelled local preview fallback.

## Build
```bash
npm run build
npm run typecheck
```

## Demo security notice
This is a developer sandbox, not a production identity provider. Signing keys and sessions are held in process memory and reset on cold starts/redeployments; serverless instances do not share memory. Do not use real credentials, production secrets, or rely on this demo for access control. Production deployments should use a durable identity provider, managed key storage/JWKS rotation, persistent session storage, rate limiting, audit logging, and strict issuer/audience validation.

## API
- `POST /api/auth` — issue token; `GET /api/auth` — list demo sessions; `POST /api/auth` with `{ "action": "revoke-all" }` — clear sessions; `DELETE /api/auth?id=...` — revoke one session.
- `POST /api/verify` — verify RS256 signature and expiration for `{ "token": "..." }`.
- `POST /api/rbac` — evaluate `{ "role": "developer", "permission": "deploy:write" }`.

Seeded demo identities: Alex Morgan (admin), Sam Rivera (developer), Jordan Lee (viewer), and Taylor Quinn (auditor).
