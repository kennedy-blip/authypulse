# AuthPulse

JWT Inspector, OAuth2/OIDC token debugging workspace, session ledger, and RBAC policy sandbox.

## Stack
Vite + React + TypeScript · Tailwind CSS v4 · Vercel Serverless Functions · Node RS256 crypto.

## Local development
```bash
npm install
npm run dev
```
For full API functionality run `vercel dev`. Vite proxies /api to localhost:3000. The UI remains usable in preview mode if the API is unavailable.

## Build
```bash
npm run typecheck
npm run build
```

## Demo security notice
This is a developer sandbox, not a production identity provider. Signing keys and sessions are held in process memory and reset on cold starts/redeployments; serverless instances do not share memory. Never use real credentials or rely on this demo for production access control. Use a managed identity provider, durable session store, managed key storage/JWKS rotation, rate limiting, audit logging, and issuer/audience validation for production.

## API
- POST /api/auth issues RS256 tokens; GET lists sessions; POST {action: revoke-all} clears sessions; DELETE /api/auth?id=... revokes one session.
- POST /api/verify validates signature and exp for {token}.
- POST /api/rbac evaluates {role, permission}.
