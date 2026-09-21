# Portfolio

My personal portfolio site, which is a single-page React/TypeScript + Vite application featuring an AI-powered chatbot that can answer questions about my work

Live: [shrravan-portfolio.vercel.app](https://shrravan-portfolio.vercel.app)

## Features

- Single-page portfolio with hero, projects, and resume sections, with smooth-scroll navigation and animated transitions using Framer Motion

- AI chatbot (hosted via the Groq API) answering questions about my experience and work

- Contact form with serverless email endpoint

- Light/dark-themed UI with responsive design, built with shadcn/ui (Radix primitives) and Tailwind CSS

## Tech stack

| Area | Tools |
|---|---|
| Framework | React 18, TypeScript, Vite 7 |
| UI | shadcn/ui (Radix UI), Tailwind CSS, Framer Motion, lucide-react |
| Routing/data fetching | React Router, TanStack Query |
| Forms | React Hook Form, Zod |
| Backend | Vercel serverless functions (src/api), Express dev proxy (src/server) |
| AI | Groq |
| Email | SendGrid / Formspree |
| Testing | Vitest, Testing Library |
| Analytics/hosting | Vercel Analytics, Vercel |

## Project structure

```text
├── api/ # Vercel serverless functions
│ ├── chat.js # Groq-backed chatbot endpoint
│ └── email.js # Contact form endpoint
├── server/ # Local Express proxy for the chatbot in dev
├── src/
│ ├── components/ # UI components
│ ├── hooks/
│ ├── lib/
│ ├── pages/ # Index.tsx, NotFound.tsx
│ └── test/
├── data/ # Content the chatbot draws from
└── public/ # Static assets
```

## Getting started

```bash
# 1. Install dependencies
npm install

# 2. Set up environment variables
cp .env.example .env

# 3. Start the dev server
npm run dev # Vite dev server (http://localhost:8080)

# 4. (optional) Run the chatbot proxy in a second terminal
npm run chat:proxy # serves the Groq chat endpoint locally
```

## Scripts

| Command | Description |
|---|---|
| npm run dev | Start the Vite dev server |
| npm run chat:proxy | Run the local Express proxy for the AI chatbot |
| npm run build | Production build |
| npm run build:dev | Development-mode build |
| npm run preview | Preview the production build locally |
| npm run lint | Run ESLint |
| npm run test | Run tests once with Vitest |
| npm run test:watch | Run tests in watch mode |

## Environment variables

See .env.example for the full list. The AI chatbot requires a Groq API key and the contact form requires its email provider key to be configured.

## Deployment

This project is deployed in Vercel. The api/ directory will be run as serverless functions in production. The server/ proxy is only used for local development.

Sources
