# NovaHost — landing + mentor portal

The NovaHost web app: the marketing landing page plus the mentor/license
dashboard, in one Vite + React SPA. Deployed on Vercel at the domain root —
signed-out visitors get the landing page (`/` and `/landing`), everything else
is behind auth.

## Stack

- Vite 5 + React 18 + TypeScript
- Tailwind CSS 3 + shadcn/ui
- react-router 6
- Supabase (`@supabase/supabase-js`) — project `epulmnfbxjmaimefhofp`

## Local development

```sh
npm install
npm run dev
```

Dev server runs on `http://localhost:8080` (and your LAN IP — `server.host` is
set to `"::"`).

## Environment

Copy `.env.example` to `.env` and fill in the values:

| Variable | Purpose |
| --- | --- |
| `VITE_SUPABASE_URL` | Supabase project URL |
| `VITE_SUPABASE_PUBLISHABLE_KEY` | Supabase anon/publishable key |
| `VITE_SUPABASE_PROJECT_ID` | Supabase project ref |
| `VITE_APK_URL` | (optional) overrides the Android APK download link |

`.env` is gitignored — never commit real keys. The service-role key must only
live in server-side environments (Supabase Edge Functions), never in this app.

## Build

```sh
npm run build   # -> dist/
```

`vercel.json` pins the framework to Vite with an SPA catch-all rewrite.

## Backend

`supabase/` holds the Edge Functions and migrations this frontend depends on.
They deploy to Supabase separately (`supabase functions deploy`), not with the
Vercel build.
