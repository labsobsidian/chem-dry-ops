# Chem-Dry of Richmond — Constants

**No secrets in this file.** API keys and tokens live in Vercel env vars and Supabase project settings.

## Client

- **Legal entity:** VACD INC
- **Service phone:** (804) 620-3050
- **Notification email (test):** Garrett's email
- **Notification email (production):** `Katies@vacdinc.com` _(swap at go-live)_

## GHL

- **Location ID:** `EtJ8aR6AulqfsgrnHJuH`
- **Inbound booking webhook:** `https://services.leadconnectorhq.com/hooks/EtJ8aR6AulqfsgrnHJuH/webhook-trigger/da6390ae-3268-41cf-bc30-e20cb8650a4f`

## Supabase

- **Project ref:** `uksswbjbizereawmdntu`
- **URL:** `https://uksswbjbizereawmdntu.supabase.co`

## Vercel

- **API base:** `https://chem-dry-stack.vercel.app`
- **Endpoints:** 7 live (see `chem-dry-stack` repo for inventory)

## n8n

- **Host:** `https://n8n.labsobsidian.co`
- **DigitalOcean droplet IP:** `134.122.124.255`
- **Cost:** $6/mo

## Public Domains

- **Booking funnel:** `chemdrybooking.labsobsidian.co`
- **Referral funnel:** `chemdryreferral.labsobsidian.co`

## External APIs

- **HCP API base:** `https://api.housecallpro.com`
- **Anthropic API:** `https://api.anthropic.com` (model: TBD per workflow)

## GHL Tags in Use

- `CD-commercial`
- `CD-duplicate-flagged`
- `CD-booking-confirmed`
- `CD-referral-reward-earned`

## Flags & Modes

- **`TEST_MODE`** in `hcp-book/route.ts` — currently `true`, flip to `false` at go-live