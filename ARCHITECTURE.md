# Chem-Dry of Richmond — Architecture

## Stack

- **Next.js** — booking funnel, referral funnel UIs
- **Vercel** — hosts the Next.js app + serverless API endpoints
- **Supabase** — Postgres database (jobs, contacts, commercial_cards, daily_cap, etc.)
- **GHL (GoHighLevel)** — CRM, pipelines, SMS, email, Conversation AI, workflows
- **HCP (Housecall Pro)** — field service management, source of truth for jobs and technicians
- **n8n** (self-hosted DigitalOcean) — scheduled and webhook-triggered automations
- **Anthropic API (Claude)** — content generation (prep emails, fuzzy matching)
- **ElevenLabs** — AI voice agent for inbound phone; bridges to HCP via Vercel middleware (in planning)
- **Stripe** — $100 deposit on booking (pending integration)
- **Inngest** — reserved for future event-driven workflows; n8n covers current needs

## Repos

- [`chem-dry-stack`](https://github.com/labsobsidian/chem-dry-stack) — the code
- [`chem-dry-ops`](https://github.com/labsobsidian/chem-dry-ops) — this repo, the command center

## Domain Topology

- **Booking funnel:** `chemdrybooking.labsobsidian.co`
- **Referral system:** `chemdryreferral.labsobsidian.co`
- **API:** `chem-dry-stack.vercel.app` (7 endpoints)
- **n8n:** `n8n.labsobsidian.co` (self-hosted DigitalOcean, $6/mo)

## Data Flow

### Booking
1. Customer lands on `chemdrybooking.labsobsidian.co`
2. 4-step funnel captures service, address, availability, confirmation
3. On submit, Vercel `/api/book` validates + POSTs to GHL inbound webhook
4. GHL workflow `CD — Booking Funnel Inbound` creates contact, assigns pipeline, fires email
5. (Future) Stripe $100 deposit collected at Step 4 before submission
6. HCP job created via middleware (`TEST_MODE=true` currently)

### Nightly Sync
1. n8n `HCP Nightly Sync` runs at 2am
2. Pulls jobs from HCP API
3. Upserts into Supabase `jobs` table
4. n8n `HCP Auto Commercial Tag` runs right after, applies `CD-commercial` tag in GHL for commercial jobs

### Referral
1. Customer clicks referral link → lands on `chemdryreferral.labsobsidian.co`
2. Generator page creates unique referral code, writes to Supabase
3. Referral link shared with prospect
4. Prospect fills referral-form → creates GHL contact with referral attribution
5. On job completion, `CD-referral-reward-earned` tag triggers reward SMS (pending)

### Duplicate Detection
1. Webhook fires on new GHL contact creation
2. n8n pulls existing GHL contacts
3. Claude API call: fuzzy match phone/name/email
4. Matches get `CD-duplicate-flagged` tag for Katie to review

## Service Responsibilities

| Domain | Source of Truth | Notes |
|--------|-----------------|-------|
| Contacts / Leads | GHL | synced bi-directionally where needed |
| Jobs / Scheduling | HCP | read into Supabase for reporting |
| Technicians | HCP | |
| Booking UX | Next.js on Vercel | |
| Referral codes | Supabase | |
| Commercial card tokens | Supabase (via Stripe) | keyed by site address |
| Daily booking cap | Supabase `daily_cap` table | to be enforced in `hcp-availability` route |

## Why this shape

See `DECISIONS.md` for the reasoning behind the big architectural choices.