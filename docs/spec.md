# Naija Civic: Spec

## Product context
Naija Civic is a web platform for Nigerians to report public issues
(roads, electricity, water, waste, security) and hold the right
authorities accountable.

**Problem:** People complain on X and WhatsApp, but complaints are
scattered and never reach the responsible office. Nobody knows who
else has the same problem or who to contact.

**Solution:** Report once, see how many others in your LGA reported
the same thing, see exactly which authority is responsible (with
phone, email, social handles), and share a ready-made post showing
the numbers to apply public pressure.

**Users:** Everyday Nigerians, mostly on budget Android phones with
slow, expensive data. Many have never used a civic app.

**Principles:** Neutral (facts and numbers, never party politics),
privacy-first (no personal data shown), nationwide from day one,
trustworthy and premium-looking but fast and simple.

**Issue status flow:** Reported, Escalated, Acknowledged, Fixed.

## Goal
Report once, see who else has the same problem, and know exactly
who to hold accountable.

## MVP screens
1. Home: hero, report button, most-reported issues, filter by
   state/LGA
2. Report form: category, map pin, photo, description
3. Issue page: details, photo, "me too" count, status, contact
   card for the responsible authority, share buttons
4. Browse: list of issues filtered by state, LGA, and category

## Contact matching
Each issue shows the most relevant contact for its category and
location: phone, email, X handle, and office address where known.
Fallback order: LGA, then state, then federal. Never a dead end.
Example: a pothole in Ikeja shows the Ikeja LGA works office first,
then the Lagos State works ministry, then FERMA if it is a federal
road.

## Sharing
- Every issue has a permanent public URL that works without login.
- Share buttons: X, WhatsApp, copy link.
- Auto-generated post text: category, location, number of reports,
  status, link, and the responsible authority's handle.
- Link previews via Open Graph tags (title, image, report count).
- Opening a shared link lands on the issue page with a clear
  "me too" action.

Example post:
"Bad road on Allen Avenue, Ikeja: 47 residents have reported this.
Status: Reported. @LagosStateGov please act. See details: <link>"

## Core tables
- states (id, name)
- lgas (id, state_id, name)
- authorities (id, name, level [federal|state|lga], state_id,
  lga_id, categories handled)
- contacts (id, authority_id, phone, email, x_handle, address,
  source_url, last_verified)
- issues (id, public_id, category, description, photo_url,
  location, lga_id, status, created_at)
- issue_votes (id, issue_id, voter_hash, created_at)

## Rules
- Contacts fall back: LGA, then state, then federal
- No accounts at first; limit reports per device/IP
- Never store or show personal data
- Neutral: show facts and numbers, not opinions
- Contacts carry a source link and a "last verified" date
- Never charge to report or escalate; no one can pay to hide or
  delay a complaint

## Build approach
Frontend first, using mock data that matches the table shapes
above. Supabase comes after the screens work.

## Out of scope for MVP
Payments, native mobile app, government dashboards
