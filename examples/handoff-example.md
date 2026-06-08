# acme-api — finish JWT auth middleware

> This is an example of what `/handoff` produces. The real file is written to your
> OS temp dir as `handoff-acme-api-2026-06-07-1840.md`, not committed to your repo.
> Names and paths below are fictional.

**Project path:** /Users/dev/work/acme-api
**Branch:** feat/jwt-auth
**Date:** 2026-06-07

## What this session did

Added JWT verification middleware to the Express API. Access tokens now validate on
every `/v1/**` route; refresh-token rotation is wired but not yet tested.

- New middleware at `src/middleware/auth.ts` (verifies `Authorization: Bearer`, attaches `req.user`).
- Protected routes in `src/routes/v1/*` via `app.use('/v1', requireAuth)`.
- Refresh flow in `src/auth/refresh.ts` — issues new pair, but the rotation/expiry test is still failing.

## Current state

- `npm test` → 38 passing, **1 failing**: `refresh.test.ts › rotates and invalidates old token`.
- The failure is a timing assumption: the test expects the old refresh token to be
  rejected immediately, but invalidation currently happens on next login, not on rotation.
- Nothing committed yet on `feat/jwt-auth` since the last green run (see `git status`).

## Next steps

1. Fix `refresh.ts` so rotation invalidates the previous refresh token at issue time, not at next login.
2. Re-run `npm test` — expect the failing rotation test to pass.
3. Add a 401 integration test for an expired access token (none exists yet).
4. Then commit `feat/jwt-auth` and open the PR against `main`.

## Key files

- src/middleware/auth.ts
- src/auth/refresh.ts
- src/routes/v1/index.ts
- test/refresh.test.ts  ← the failing one

## Don't repeat

- Token secret + config decisions already live in `docs/adr/0007-auth.md` — read it, don't re-derive.
- The route-protection approach was settled in PR #142 (linked in that ADR).

## Suggested skills

- `superpowers:systematic-debugging` — to work the failing rotation test methodically
- `superpowers:test-driven-development` — for the new expired-token integration test
