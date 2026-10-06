# BizcaiaOS

AI-Powered Land Acquisition Operating System (LAOS).

**BizcaiaOS is developed using a document-driven engineering process. Product decisions, architecture, implementation, integration, and QA are intentionally separated. The repository—not chat history—is the authoritative source of truth.**

### For AI assistants

**Start here:** [`docs/AI_SESSION_START.md`](docs/AI_SESSION_START.md)

Governance lives in `docs/` — see [`docs/DOCUMENTATION_INDEX.md`](docs/DOCUMENTATION_INDEX.md). Engineering Playbook, Development Tasks, handoffs, module business rules, database ADRs (`04_Database_Architecture.md`), and the knowledge framework (`docs/architecture/`, `docs/domain/`, `docs/playbooks/`). Do not invent domain methodology; do not implement from chat memory.

## Stack

- Next.js (App Router) + React + TypeScript
- Tailwind CSS
- Supabase (PostgreSQL, Auth, Storage)

## Local Setup

1. Install dependencies:

   ```bash
   npm install
   ```

2. Start the local Supabase stack (requires Docker):

   ```bash
   supabase start
   ```

3. Copy environment variables:

   ```bash
   cp .env.local.example .env.local
   ```

   Fill in `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`, and `SUPABASE_SERVICE_ROLE_KEY` from the output of `supabase status`.

4. Run the dev server:

   ```bash
   npm run dev
   ```

5. App runs at `http://localhost:3000`. Local Supabase Studio runs at the URL printed by `supabase status`.

## Database

All schema changes live in `supabase/migrations/`, applied in numeric order. Do not hand-edit an already-applied migration — add a new one instead (see `docs/04_Database_Architecture.md`, Migration Strategy).

To reset the local database to match all migrations from scratch:

```bash
supabase db reset
```

## Project Structure

```
app/         Next.js App Router pages/routes
components/  Shared, reusable UI components
features/    Feature-scoped modules (e.g. properties, negotiations)
lib/         Shared utilities, Supabase clients
supabase/    Migrations, config, and local Supabase CLI state
docs/        Single source of truth — start with AI_SESSION_START.md
  architecture/   Product/knowledge ADRs (ADR-034+)
  domain/         Field knowledge & acquisition patterns
  playbooks/      How people execute acquisition (procedures TBD)
  <module>/       Module business rules (ownership, timeline, documents, …)
```
