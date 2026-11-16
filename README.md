# FlagPulse

Full-stack feature flag control plane, canary rollout manager, and deterministic user-context evaluator. Built with Vite, React, TypeScript, Tailwind CSS v4, and Vercel Serverless Functions.

## Development

`npm install && npm run dev` starts Vite. The client falls back to local demo data if API routes are unavailable. Run `npx vercel dev` to test serverless endpoints locally.

## Vercel

Import this repository. Build command: `npm run build`; output directory: `dist`. No environment variables are required for the seeded demo.

## API

- `GET /api/flags` lists flags and audit events.
- `POST /api/flags` creates a flag.
- `PATCH /api/flags` updates toggle, rollout, and targeting rules.
- `POST /api/evaluate` evaluates `{ userId, tier, region, environment }`.

The SHA-256-derived bucket is stable for each flag/user pair. A flag must pass its master switch, environment, targeting segments, and rollout percentage.

**Persistence warning:** the requested in-memory store is ephemeral on Vercel and is not durable or shared across function instances. Replace `api/_store.ts` with a database/KV adapter before relying on it as a production control plane.
