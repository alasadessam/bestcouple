# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **Frontend**: React + Vite (couple-zone)

## Structure

```text
artifacts-monorepo/
├── artifacts/              # Deployable applications
│   ├── api-server/         # Express API server
│   └── couple-zone/        # React+Vite couple app (frontend)
├── lib/                    # Shared libraries
│   ├── api-spec/           # OpenAPI spec + Orval codegen config
│   ├── api-client-react/   # Generated React Query hooks
│   ├── api-zod/            # Generated Zod schemas from OpenAPI
│   └── db/                 # Drizzle ORM schema + DB connection
├── scripts/                # Utility scripts (single workspace package)
├── pnpm-workspace.yaml     # pnpm workspace
├── tsconfig.base.json      # Shared TS options
├── tsconfig.json           # Root TS project references
└── package.json            # Root package with hoisted devDeps
```

## App: منطقة الأزواج (Couple Zone)

A luxury private couple zone app with:
- JWT auth (bcryptjs passwords)
- Pair code system for linking two accounts
- Chat/messages between partners
- Virtual gifts (12 types)
- 10 couple games (Truth/Dare, Positions Wheel, Mood Picker, Couples Quiz, etc.)
- Game invitations system
- RTL Arabic UI with dark romantic theme
- PWA manifest for mobile installation

### Routes
- `GET /api/auth/me` — current user
- `POST /api/auth/register` — register
- `POST /api/auth/login` — login
- `POST /api/auth/logout` — logout
- `POST /api/auth/pair` — pair with partner via code
- `GET/POST /api/messages` — messages
- `POST /api/messages/:id/react` — react to message
- `GET/POST /api/gifts` — gifts
- `GET /api/games` — list games
- `POST /api/games/:id/play` — get random game card
- `GET/POST /api/invites` — game invitations
- `POST /api/invites/:id/accept` — accept invite

## DB Schema
- `users` — id, username, password_hash, display_name, avatar, pair_code, partner_id
- `sessions` — id, user_id, token
- `messages` — id, sender_id, receiver_id, content, type, reaction
- `gifts` — id, sender_id, receiver_id, gift_type, gift_emoji, gift_name, message
- `game_invites` — id, game_id, game_name, game_emoji, sender_id, receiver_id, status
