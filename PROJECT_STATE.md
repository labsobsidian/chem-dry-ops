# Chem-Dry of Richmond — Project State

**Last Updated:** 2026-04-20

## Mission

Build an AI-forward ops stack for Chem-Dry of Richmond (VACD INC) that automates booking intake, referral generation, prep communication, and reporting — all routed through a redeployable monorepo template that will be forked for future Obsidian Labs home-service clients. Chem-Dry is the reference implementation for the agency's productized offering.

## Primary Contacts

- **Brian Curran** — CEO, VACD INC
- **Katie** — Marketing (day-to-day operator), `Katies@vacdinc.com`

## Current Phase

**Phase 2 — Integration & Automation.** Core infrastructure is live. Automations and reporting layer in progress. Go-live pending remaining items + launch checklist.

## Completed

### Infrastructure
- GitHub monorepo `chem-dry-stack` with `config/client.json` for redeployability
- Supabase schema deployed (9 tables with RLS policies, 100 HCP jobs synced)
- All 7 Vercel API endpoints live
- Booking funnel live end-to-end at `chemdrybooking.labsobsidian.co` (4 steps)
- Referral system live end-to-end at `chemdryreferral.labsobsidian.co` (3 pages)
- GHL sub-account created and configured
- n8n self-hosted on DigitalOcean

### GHL Workflows
- `CD — Booking Funnel Inbound` (Draft mode — handles webhook, creates contact, assigns to pipeline, fires email notification)

### n8n Workflows
- `HCP Nightly Sync` — 2am daily, syncs HCP jobs to Supabase (published)
- `HCP Auto Commercial Tag` — nightly, applies `CD-commercial` tag in GHL (published)
- `Duplicate Detection` — webhook trigger, pulls GHL contacts, Claude API fuzzy match, applies `CD-duplicate-flagged` tag (published)

## Active Work

_(None currently in progress — waiting on prioritization of the remaining build order.)_

## Remaining

Ordered by priority.

### GHL Automations (3)
1. **Review-to-Referral SMS** — fires 30 minutes after customer clicks review link, sends referral generator SMS
2. **Referral Reward SMS** — triggers on `CD-referral-reward-earned` tag, sends $50 reward SMS
3. **Daily Cap Alert** — notifies Katie when daily booking cap is reached

### Other Workstreams
4. **Prep Email Generator** — n8n workflow, triggers on `CD-booking-confirmed` tag, calls Claude API for personalized pre-appointment email, sends via GHL
5. **Stripe $100 Deposit** — blocked on Brian/Katie providing Stripe keys; once received: add to Vercel env vars, wire `/api/stripe-deposit`, add Stripe.js to Step 4 of booking funnel
6. **Reporting Dashboard** — pulls from Supabase `jobs` table, shows revenue by tech, busiest days, commercial vs residential split
7. **Daily Cap Enforcement** — wire existing Supabase `daily_cap` table into `hcp-availability` route
8. **Commercial Cards** — Stripe tokens stored in Supabase `commercial_cards` table keyed by site address
9. **Multi-site Search** — custom tool for Katie to search sites across commercial accounts
10. **Conversation AI** — GHL native, configure for Chem-Dry persona
11. **`chem-dry-redeploy` skill** — meta-step: extract the redeploy pattern into a skill in `obsidian-labs-skills` so forking for a new location is fast

## Blockers

- **Stripe integration** — awaiting publishable + secret keys from Brian/Katie
- **Go-live items** — see `GO_LIVE_CHECKLIST.md`

## Recently Archived

_(none yet — archive completed sections here when PROJECT_STATE grows past ~500 lines)_
