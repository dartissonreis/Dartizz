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
- **Real-time**: Socket.io (server + client)

## Application: Kahoot Clone

A real-time multiplayer quiz game similar to Kahoot.

### Features
- **Quiz creation**: Teacher creates quizzes with multiple questions, 4 colored options, correct answer, and time limit
- **Lobby**: Generates 6-digit PIN, shows players joining in real time
- **Player game screen**: Large colored buttons (red triangle, blue diamond, yellow circle, green square)
- **Speed-based scoring**: Points calculated by correctness + speed (max 1000 pts/question)
- **Live leaderboard**: Rankings updated after each question, final podium at end

### Pages
- `/` — Home landing page
- `/create` — Quiz creation form
- `/quizzes` — List of created quizzes
- `/join` — Player join screen (PIN + nickname)
- `/lobby/:pin` — Host lobby with PIN display and player list
- `/host/:pin` — Host game control screen
- `/play/:pin` — Player game screen with colored answer buttons
- `/ranking/:pin` — Final leaderboard

### Architecture
- **Frontend**: React + Vite + Tailwind CSS (`artifacts/kahoot-clone`)
- **Backend**: Express 5 + Socket.io (`artifacts/api-server`)
- **Database**: PostgreSQL with tables: `quizzes`, `questions`, `games`, `game_players`
- **Real-time**: Socket.io mounted at `/socket.io` path

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
