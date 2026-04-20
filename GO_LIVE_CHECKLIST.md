# Chem-Dry of Richmond — Go-Live Checklist

Items that must be true before the system is live in production.

## Code Flags

- [ ] Flip `TEST_MODE = false` in `hcp-book/route.ts` and push to main
- [ ] Verify `TEST_MODE` is respected in all other endpoints (audit)

## GHL

- [ ] Publish `CD — Booking Funnel Inbound` workflow (currently Draft)
- [ ] Swap notification email from Garrett's to `Katies@vacdinc.com`
- [ ] Confirm all 3 pending automations are published (Review-to-Referral, Referral Reward, Daily Cap Alert)
- [ ] Conversation AI persona configured and tested

## Stripe

- [ ] Brian/Katie provide Stripe publishable + secret keys
- [ ] Keys added to Vercel env vars (both preview and production)
- [ ] `/api/stripe-deposit` endpoint wired and tested
- [ ] Stripe.js added to Step 4 of booking funnel
- [ ] Test transaction run end-to-end

## Reporting

- [ ] Reporting dashboard populated from Supabase `jobs` table
- [ ] Katie has access and has been walked through it

## Communications

- [ ] Prep Email Generator live and sending on `CD-booking-confirmed` tag
- [ ] Daily Cap Enforcement wired into `hcp-availability` route

## Final

- [ ] End-to-end test booking (real customer flow in prod)
- [ ] Katie signs off
- [ ] Monitor first 48 hours actively