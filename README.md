Shrravan Bala · Portfolio
Vite (https://vitejs.dev)
React (https://react.dev)
TypeScript (https://www.typescriptlang.org/)
Tailwind CSS (https://tailwindcss.com/)
shadcn/ui (https://ui.shadcn.com/)
Framer Motion (https://www.framer.com/motion/)
Groq (https://groq.com/)
Vercel (https://vercel.com)
An interactive personal portfolio built with React, featuring a dynamic particle background, an AI-powered assistant, dark/light mode, and full offline support.
Features
- Splash Screen — Animated entry gate that greets visitors once per session
- Particle Background — Canvas-based particle system with mouse repulsion and connecting lines
- Cursor Glow — Smooth radial glow that follows the cursor
- Dark / Light Mode — Persisted toggle that respects prefers-color-scheme
- Dynamic Accent Color — Pick from 6 accent hues (blue, red, green, orange, purple, pink) — recolours the entire UI via CSS variables
- Glassmorphism UI — Frosted glass panels, glow borders, and subtle grid background
- Scroll Animations — Every section fades and slides in as you scroll (Framer Motion)
- 3D Tilt Portrait — Hero image rotates with spring physics based on mouse position
- AI Chat Assistant — Floating widget powered by Groq LLM, preloaded with portfolio context; supports round-robin API key rotation
- Contact Form — Validated form (react-hook-form + zod) sent via Formspree
- Animated Skill Bars — Gradient-filled progress bars that animate on scroll
- Service Worker — Offline caching for static assets and runtime resources
- Responsive Design — Fully responsive layout with mobile-optimised navigation
- Interest Prompt — Non-intrusive "get in touch" call-to-action after 3 minutes of browsing
Tech Stack
Layer	Technology
Build	Vite 7
Frontend	React 18, TypeScript 5
Routing	React Router DOM v6
Styling	Tailwind CSS 3, PostCSS
UI Library	shadcn/ui (Radix UI primitives)
Animations	Framer Motion 12
Charts	Recharts
Carousel	Embla Carousel
Forms	react-hook-form + zod
Icons	Lucide React
Theming	next-themes
Data Fetching	TanStack React Query 5
AI Backend	Groq API (LLM)
Email	Formspree
Analytics	@vercel/analytics
Testing	Vitest + Testing Library
Linting	ESLint 9 + typescript-eslint
Offline	Custom Service Worker
Sections
- Hero — Name, tagline, links, 3D tilt portrait, scroll indicator
- About — Bio with highlight cards
- Projects — Project cards with cover images, tags, and links
- Resume — Experience, education, skills (categorised), certifications, extracurriculars
- Skills — Animated proficiency bars (out of 10)
- Contact — Contact form + footer
Getting Started
# Clone the repository
git clone https://github.com/Error403Allowed/portfolio.git
cd portfolio

# Install dependencies
npm install

# Copy environment variables and fill in your keys
cp .env.example .env
Required environment variables:
Variable	Description
GROQ_API_KEY_1	Groq API key (get one at console.groq.com (https://console.groq.com))
GROQ_API_KEY_2	Optional second key for round-robin load balancing
FORMSPREE_ENDPOINT	Formspree form endpoint (e.g. https://formspree.io/f/yourFormId)
GROQ_MODEL	Groq model ID (defaults to meta-llama/llama-4-scout-17b-16e-instruct)
CHAT_ALLOWED_ORIGIN	CORS origin for local dev (defaults to http://localhost:8080)
# Start the dev server (API proxy runs via Vite middleware — no separate process needed)
npm run dev
Open http://localhost:8080 (http://localhost:8080) in your browser.
Scripts
Command	Description
npm run dev	Start Vite dev server with API middleware
npm run build	Production build
npm run preview	Preview production build
npm run test	Run Vitest test suite
npm run lint	Run ESLint
npm run chat:proxy	Standalone Groq proxy server
Project Structure
src/
├── App.tsx                  # Root component with router
├── main.tsx                 # Entry point + service worker registration
├── index.css                # Global styles, CSS variables, utilities
├── components/
│   ├── sections/            # Hero, About, Projects, Resume, Skills, Contact
│   ├── ui/                  # shadcn/ui primitives (~40 components)
│   ├── ParticleBackground.tsx
│   ├── Navbar.tsx
│   ├── SplashScreen.tsx
│   ├── ColorPicker.tsx
│   ├── CursorGlow.tsx
│   ├── PortfolioAssistantWidget.tsx
│   └── ...
├── pages/
│   ├── Index.tsx            # Main portfolio page
│   └── NotFound.tsx         # 404 page
├── hooks/                   # use-mobile, use-toast
├── lib/                     # Utility functions (cn)
└── test/                    # Vitest setup and tests

data/
└── portfolio.json           # Structured content (source of truth for AI context)

server/
├── groqHandler.mjs          # Groq API handler with key rotation
├── emailHandler.mjs         # Formspree email proxy
├── portfolioContext.mjs     # Builds AI system prompt from portfolio.json
└── groqProxy.mjs            # Standalone proxy server

api/                         # Vercel serverless functions
├── chat.js
└── email.js

public/
└── sw.js                    # Service Worker (offline caching)
Deployment
The project is ready to deploy on Vercel. Serverless functions in the api/ directory handle the chat and email endpoints automatically.
Deploy with Vercel (https://vercel.com/new)
Make sure to set the same environment variables in your Vercel project settings.
