# Portfolio

My personal portfolio site — a single-page app built with React, TypeScript, and Vite, with an AI chatbot that can answer questions about my work.

**Live:** [shrravan-portfolio.vercel.app](https://shrravan-portfolio.vercel.app)

## Features

- **Single-page portfolio** — hero, projects, and resume sections with smooth-scroll navigation and Framer Motion animations.
- **AI chatbot** — a Groq-backed assistant that answers questions about my background and projects.
- **Contact form** — sends messages via a serverless email endpoint.
- **Responsive, themed UI** — built with shadcn/ui (Radix primitives) and Tailwind CSS, with light/dark support.

## Tech stack

| Area | Tools |
|------|-------|
| Framework | React 18, TypeScript, Vite 7 |
| UI | shadcn/ui (Radix UI), Tailwind CSS, Framer Motion, lucide-react |
| Routing / data | React Router, TanStack Query |
| Forms | React Hook Form, Zod |
| Backend | Vercel serverless functions (`api/`), Express dev proxy (`server/`) |
| AI | Groq |
| Email | SendGrid / Formspree |
| Testing | Vitest, Testing Library |
| Analytics / hosting | Vercel Analytics, Vercel |

## Project structure

```
├── api/                # Vercel serverless functions
│   ├── chat.js         # Groq-backed chatbot endpoint
│   └── email.js        # Contact form endpoint
├── server/             # Local Express proxy for the chatbot in dev
├── src/
│   ├── components/      # UI components
│   ├── hooks/
│   ├── lib/
│   ├── pages/           # Index.tsx, NotFound.tsx
│   └── test/
├── data/               # Content the chatbot draws from
└── public/             # Static assets
```

## Getting started

```bash
# 1. Install dependencies
npm install

# 2. Set up environment variables
cp .env.example .env

# 3. Start the dev server
npm run dev            # Vite dev server (http://localhost:5173)

# 4. (optional) Run the chatbot proxy in a second terminal
npm run chat:proxy     # serves the Groq chat endpoint locally
```

## Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start the Vite dev server |
| `npm run chat:proxy` | Run the local Express proxy for the AI chatbot |
| `npm run build` | Production build |
| `npm run build:dev` | Development-mode build |
| `npm run preview` | Preview the production build locally |
| `npm run lint` | Run ESLint |
| `npm run test` | Run tests once with Vitest |
| `npm run test:watch` | Run tests in watch mode |

## Environment variables

See `.env.example` for the full list. The AI chatbot needs a Groq API key, and the contact form needs its email provider key configured.

## Deployment

Deployed on Vercel. The `api/` directory runs as serverless functions in production; the `server/` proxy is only used for local development.
