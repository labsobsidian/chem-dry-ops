# CLAUDE.md — Chem-Dry of Richmond (chem-dry-ops)

You are working on the Chem-Dry of Richmond AI ops stack, built by Obsidian Labs (Garrett).

This is an Atlas by Obsidian Labs deployment — the AI operating system for Chem-Dry of Richmond (VACD INC), a carpet and upholstery cleaning franchise in Richmond, Virginia.

---

## Always read first

1. `PROJECT_STATE.md` — what's built, what's in progress, what's next
2. `CONSTANTS.md` — GHL location ID, Supabase ref, Vercel endpoints, tags
3. `ARCHITECTURE.md` — stack, data flows, service responsibilities
4. `DECISIONS.md` — architectural decisions with context and reasoning

---

## The Working Loop

```
Problem → Method → Approval → Build → Update State → (maybe) Skillify
```

Never skip Method or Update State. Even for small changes.

---

## Project Context

**Client:** Chem-Dry of Richmond (VACD INC)
**Contacts:** Brian Curran (CEO), Katie (marketing, day-to-day operator — Katies@vacdinc.com)
**Current phase:** Phase 2 — Integration & Automation
**Reference implementation:** This is the flagship Atlas deployment — the pattern all future clients follow

---

## Repo Structure

```
chem-dry-ops/
├── PROJECT_STATE.md      ← Source of truth
├── ARCHITECTURE.md       ← Stack, data flows, domain topology
├── CONSTANTS.md          ← GHL location ID, Supabase ref, all endpoints
├── DECISIONS.md          ← Append-only decisions log
├── GO_LIVE_CHECKLIST.md  ← Pre-launch punch list
├── .skills-version       ← Pins obsidian-labs-skills at v0.2.0
└── CLAUDE.md             ← This file
```

Code lives in: `labsobsidian/chem-dry-stack` (Next.js/Vercel/Supabase)

---

## Stack

| Layer | Tool | Status |
|---|---|---|
| Booking funnel | chemdrybooking.labsobsidian.co | Live |
| Referral system | chemdryreferral.labsobsidian.co | Live |
| API | chem-dry-stack.vercel.app (7 endpoints) | Live |
| Database | Supabase (9 tables, RLS policies) | Live |
| CRM | GoHighLevel sub-account | Live |
| Job management | HCP (Housecall Pro) | Live — API integrated |
| Automation | n8n (DigitalOcean, $6/mo) | Live — 3 workflows published |
| AI | Anthropic API (Claude) | Live — duplicate detection |
| Voice | ElevenLabs | Planned |
| Payments | Stripe | Blocked — awaiting keys from Brian/Katie |

---

## Key Constants

| Constant | Value |
|---|---|
| GHL Location ID | EtJ8aR6AulqfsgrnHJuH |
| Supabase project ref | uksswbjbizereawmdntu |
| Supabase URL | https://uksswbjbizereawmdntu.supabase.co |
| Vercel API base | https://chem-dry-stack.vercel.app |
| Booking funnel | chemdrybooking.labsobsidian.co |
| Referral funnel | chemdryreferral.labsobsidian.co |
| n8n host | https://n8n.labsobsidian.co |
| TEST_MODE | true — flip to false at go-live |
| Notification email (prod) | Katies@vacdinc.com |

See CONSTANTS.md for complete list including GHL tags and webhook URLs.

---

## What's Built

- GitHub monorepo `chem-dry-stack` with `config/client.json`
- Supabase schema: 9 tables with RLS, 100 HCP jobs synced
- 7 Vercel API endpoints live
- 4-step booking funnel live
- 3-page referral system live
- GHL sub-account configured
- n8n on DigitalOcean
- 3 n8n workflows: HCP Nightly Sync, Auto Commercial Tag, Duplicate Detection

## Remaining Work (Priority Order)

1. Review-to-Referral SMS workflow (GHL)
2. Referral Reward SMS workflow (GHL)
3. Daily Cap Alert (GHL)
4. Prep Email Generator (n8n + Claude API)
5. Stripe $100 deposit — BLOCKED awaiting keys
6. Reporting Dashboard (Supabase jobs table)
7. Daily Cap Enforcement (hcp-availability route)
8. Commercial Cards (Stripe + Supabase)
9. Multi-site Search
10. Conversation AI (GHL native)
11. ElevenLabs Voice Agent

## Blockers

- Stripe keys — awaiting from Brian/Katie
- TEST_MODE still true in hcp-book/route.ts
- CD — Booking Funnel Inbound workflow still in Draft mode
- Notification email still set to Garrett's (swap to Katies@vacdinc.com at go-live)

---

## GHL Tags in Use

- `CD-commercial`
- `CD-duplicate-flagged`
- `CD-booking-confirmed`
- `CD-referral-reward-earned`

---

## Conventions

- Never invent constants — all values in CONSTANTS.md
- Never commit secrets — keys live in Vercel/Supabase env vars
- TEST_MODE=true means no real HCP bookings — do not flip until go-live checklist complete
- Update PROJECT_STATE.md every session
- Log architectural decisions in DECISIONS.md

## Tone

Direct, concrete, no filler. Garrett runs fast. Propose before building. Flag risk. Push back on bad ideas.
