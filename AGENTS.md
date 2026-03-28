# AGENTS.md

This file supplements `CLAUDE.md` for Codex-style agents working in this repository.

## Purpose

`Siftly` is a self-hosted Twitter/X bookmark manager with AI-powered categorization, search, and mindmap visualization.

Treat this as a standalone application repository. Do not couple changes here to other local workspace projects unless the user explicitly asks for that.

## Working Mode

- Prefer small, targeted fixes over broad refactors.
- Keep upstream compatibility high because this repository is a fork of `viperrcrypto/Siftly`.
- Before changing behavior, inspect existing import paths and keep fallback values consistent across import flows.

## Verified Local Setup

These commands were verified in this fork on 2026-03-28:

```bash
npm install
npx prisma generate
touch prisma/dev.db
npx prisma db push
npm run build
```

## Known Setup Note

- On this machine, `prisma migrate dev --name init` failed on a fresh clone with a generic schema engine error before the SQLite file existed.
- Creating `prisma/dev.db` first and then running `npx prisma db push` worked.
- After `db push`, `migrate dev` reports drift unless the database is reset, so prefer the verified setup path above for first boot.

## Verification

Use these commands before calling work complete:

```bash
npx prisma generate
npx prisma db push
npm run build
```

Add more targeted verification when touching:

- OAuth import routes
- Prisma schema or migrations
- AI provider/auth flows
- bookmark import and export paths

## Safe Edit Boundaries

- `app/` for routes and UI
- `lib/` for parsing, auth, AI, search, and integration logic
- `prisma/` for schema and migrations

Be careful when editing:

- `lib/claude-cli-auth.ts`
- `lib/openai-auth.ts`
- `lib/codex-cli.ts`
- `app/api/import/**`
- `prisma/schema.prisma`

## Security And Data Rules

- Never commit `.env`, `.env.local`, API keys, OAuth tokens, or bookmark database files.
- Treat `prisma/dev.db` as private user data.
- Do not hardcode secrets into routes, settings defaults, or test fixtures.

