# VULNEX — Stage 1 Frontend Preview

Frontend-only implementation for VULNEX. This stage contains the design system, responsive application shell, route navigation, page layouts, local demo interactions, and typed API contracts. It does **not** run real scans or connect to a backend.

## Requirements
- Node.js 20+
- npm 10+

## Run locally
```bash
npm ci
npm run dev
```

## Validation
```bash
npm run lint
npm run typecheck
npm run build
```

## Routes
- `/` Dashboard
- `/projects`, `/projects/:id`
- `/scans/new`, `/scans`, `/scans/:id`
- `/findings`, `/findings/:id`
- `/reports`
- `/auth/sign-in`, `/auth/sign-up`, `/auth/forgot-password` (UI preview only)
- `/ai-repair` (Stage 3 preview; disabled)
- `/approvals` (Stage 3 placeholder)
- `/integrations`
- `/activity`, `/settings`

## Demo-data disclosure
The workspace is explicitly marked DEMO. Dashboard metrics, projects, findings, scan history, evidence, reports, and activity are synthetic examples. Creating a project only updates local React state; it does not upload a ZIP, contact GitHub, launch a scan, or persist data to a server. Authentication screens also remain preview-only until the backend is implemented.

## Stage 1 scope
- Responsive dashboard, project list/detail, scan creation/history/detail, findings list/detail, reports, AI repair preview, approval center, GitHub integrations, activity log, settings, and auth screen layouts.
- Local interactions: navigation, project creation preview, URL/repository/ZIP input validation, scope/profile fields, findings search/filter/sort/pagination, finding status changes, sample-log disclosure, JSON/CSV export, and profile/notification controls.
- Backend-only features are explicitly marked as planned or disabled; no live scanner, upload, OAuth, authentication, AI patching, or approvals are claimed.

## Architecture
- `src/App.tsx`: application shell, routes, page components, local demo interactions.
- `src/index.css`, `src/app.css`: design tokens and responsive visual system.
- `src/lib/api/contracts.ts`: typed domain models and endpoint map for Stage 2.
- `src/lib/api/client.ts`: typed HTTP client scaffold for Stage 2.
- `src/lib/utils.ts`: formatting, download, URL validation helpers.

Stage 2 should replace the demo provider with API-backed data without changing the page design or domain contracts unnecessarily.

## Deploy to Cloudflare Pages (free tier)
1. Push the **contents** of this folder to the root of a new GitHub repository.
2. In Cloudflare, open **Workers & Pages → Create → Pages → Connect to Git**.
3. Select the repository and set:
   - Framework preset: `Vite`
   - Build command: `npm run build`
   - Build output directory: `dist`
   - Root directory: `/`
4. Deploy. The `public/_redirects` file keeps client-side routes working on direct page refreshes.

The project has no required environment variables in Stage 1. Do not add API secrets or service-role keys to this frontend repository.

## Before calling Stage 1 verified
Run `npm ci`, `npm run lint`, `npm run typecheck`, and `npm run build` in an environment with working npm registry access. Then manually test desktop and mobile layouts, all navigation routes, forms, filters, status changes, and JSON/CSV downloads. A successful source syntax check alone is not a substitute for these checks.
