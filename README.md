# Analogix

> Do you really need to have a lot of tabs open when you can have everything in one place with Analogix? You will not have to switch between tools like claude, quizlet and anki anymore.

![Platform](https://img.shields.io/badge/platform-web%20%7C%20mobile%20%7C%20api-6366f1)

![Node](https://img.shields.io/badge/node-%3E%3D22%20%3C27-339933)

![npm](https://img.shields.io/badge/npm-%3E%3D11-CC3534)

---

## Table of Contents

- [Screenshots](#screenshots)

- [The story behind Analogix](#the-story-behind-analogix)

- [Architecture](#architecture)

- [The apps](#the-apps)

- [Getting started](#getting-started)

- [Environment variables](#environment-variables)

- [Root-level scripts](#root-level-scripts)

- [Further reading](#further-reading)

---

## Screenshots

| Mobile Dashboard | Chat | Web Dashboard |

|:---:|:---:|:---:|

| ![Mobile Dashboard](screenshots/mobile-dashboard.png) | ![Chat](screenshots/mobile-chat.png) | ![Web Dashboard](screenshots/web-dashboard.png)

| Study Hub | Calendar | Timer |

![Study Hub](screenshots/mobile-studyhub.png) | ![Calendar](screenshots/mobile-calendar.png) | ![Timer](screenshots/mobile-timer.png) |

| Quiz | | |

| ![Quiz](screenshots/mobile-quiz.png) | |

---

## Features

- **AI Tutor:** Analogix has an AI Tutor that is backed by Groq. The AI Tutor explains concepts to you generates quizzes and flashcards from the material you are studying.

- **Flashcards:** Analogix has flashcards with SM-2 spaced repetition. You can create your flashcards or let the AI build a set from an uploaded file or chat session.

- **Quizzes:** Analogix has quizzes with choice, essay or mixed questions. The quizzes can be. Untimed. The AI generates the quizzes from the content you are studying.

- **Calendar:** Analogix has a calendar with day, week or month view. The calendar auto-calculates term dates for every state and imports ICS from school portals.

- **Timer:** Analogix has a Pomodoro timer with session and streak tracking.

- **Study Schedule:** Analogix generates a study plan from your subjects and deadlines. You can edit the study plan if you need to.

- **Subjects:** Analogix helps you track your marks, homework and syllabus. It also has a built-in document editor.

- **Rooms:** Analogix has real-time group work with chat, documents and a synced timer.

- **Formulas:** Analogix has subject-based formula sheets rendered in LaTeX. You can search for formulas if you need to.

- **Achievements:** Analogix has XP. Badges to make studying more fun.

- **Assessment Guide:** You can hand the AI an assessment PDF. It drafts a study plan for you.

---

## Architecture

```

┌───────────────────────┐

│ AnalogixWeb │

│ Next.js 16. Turbopack │

│ REST + GraphQL client │

└────────┬──────────────┘

│ HTTP/WS

┌────────▼──────────────┐

│ AnalogixGraphQL │

│ Apollo Server v5 │◄──── Supabase Auth (JWT)

│ Express 5 + graphql-ws│ Groq AI, OpenAlex

│ Redis PubSub │ Supabase DB/Storage

└───────┬──────────────┘

│ HTTP/WS

┌────────▼──────────────┐

│ AnalogixMobile │

│ Expo SDK 54 + RN 0.81 │

│ Material 3 Expressive │

└───────────────────────┘

```

Analogix made some key design decisions.

Analogix decided that the web and mobile Analogix will share the GraphQL API.

This means that there will be no endpoints.

Analogix also decided that auth will be handled server-side via Supabase JWT verification.

Analogix decided to use Redis PubSub to manage subscriptions for room sync and chat streaming.

This falls back to in-process in dev.

Both clients share types and schemas from `@analogix/shared`.

If you change a Zod schema the rest follows.

---

## The apps

| Package Description | Tech stack |

|---------|-------------|------------|

| `AnalogixWeb` | Web client | Next.js 16 Turbopack, TypeScript |

| `AnalogixMobile` Mobile app | React Native 0.81 (Expo SDK 54) react-native-paper Reanimated 4 |

| `AnalogixGraphQL` | BFF / GraphQL gateway | Apollo Server v5, Express 5 graphql-ws, Redis |

@analogix/shared` | Common types and schemas | TypeScript, Zod, JSON manifests |

| `@analogix/mcp` | Model Context Protocol server | TypeScript exposes app data via MCP |

---

## Getting started

```bash

# 1. Install. Workspace dependencies

npm install

# 2. Copy environment templates. Add your secrets

cp AnalogixGraphQL/.env.example AnalogixGraphQL/.env

cp AnalogixMobile/.env.example AnalogixMobile/.env

# 3. Build the shared package first (required by all workspaces)

npm run build:shared

# 4. Start the API (terminal 1)

npm run dev:api # http://localhost:4000/graphql

# 5. Start the web client (terminal 2)

npm run dev:web # http://localhost:3000

# 6. Start the app (terminal 3)

npm run dev:mobile # Expo dev server

```

---

## Environment variables

**AnalogixGraphQL/.env** (Server runtime)

`PORT` `NODE_ENV` `CORS_ORIGINS` `SUPABASE_URL` `SUPABASE_ANON_KEY` `SUPABASE_SERVICE_ROLE_KEY` `GROQ_API_KEY` `GROQ_API_KEY_2` `GOOGLE_CLIENT_ID` `GOOGLE_CLIENT_SECRET` `DESMOS_API_KEY` `REDIS_URL` `LOG_LEVEL`

**AnalogixMobile/.env** (Client side)

`EXPO_PUBLIC_SUPABASE_URL` `EXPO_PUBLIC_SUPABASE_ANON_KEY` `EXPO_PUBLIC_GRAPHQL_HTTP_URL` `EXPO_PUBLIC_GRAPHQL_WS_URL` `EXPO_PUBLIC_GOOGLE_*_CLIENT_ID` `EXPO_PUBLIC_GOOGLE_REDIRECT_SCHEME`

**AnalogixWeb/.env.local** (Next.js)

`GROQ_API_KEY` `GROQ_API_KEY_2` `NEXT_PUBLIC_SUPABASE_URL` `NEXT_PUBLIC_SUPABASE_ANON_KEY` `SUPABASE_SERVICE_ROLE_KEY` `GOOGLE_CLIENT_ID` `GOOGLE_CLIENT_SECRET` `NEXT_PUBLIC_SITE_URL` `DESMOS_API_KEY` `ALLOW_DEV_API`

---

## Root-level scripts

Command | Function |

|---------|----------|

| `npm run dev` | Starts all workspaces in dev mode |

| `npm run dev:api` | GraphQL BFF on `:4000` |

| `npm run dev:web` | Next.js dev server on `:3000` |

| `npm run dev:mobile` | Expo dev client on `:8081` |

| `npm run dev:shared` | Watches `@analogix/shared` for changes |

| `npm run build` | Builds all workspaces in dependency order |

| `npm run build:shared` | Builds shared package first

| `npm run typecheck` | `tsc --noEmit` across all workspaces |

| `npm run lint` | Run ESLint |

| `npm run clean` | Clears `dist/` `.next/` etc. |

---

## Further reading

You can refer to the READMEs in each package for more details:

- [`AnalogixGraphQL/README.md`](./AnalogixGraphQL/README.md). Schema, resolvers, deployment.

- [`AnalogixMobile/README.md`](./AnalogixMobile/README.md). Screenshots, theming EAS builds, auth.

- [`AnalogixWeb/README.md`](./AnalogixWeb/README.md). Setup, pages, troubleshooting.

---

## License

Analogix is a project. All rights reserved.

---

*Disclaimer: While AI has been of assistance in putting portions of the code it has all been fact and bug-checked to provide the best experience, for users of Analogix.*