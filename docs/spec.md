# Naija Civic: Spec

## Goal
Report once, see who else has the same problem, and know exactly
who to hold accountable.

## MVP screens
1. Home: most-reported issues, filter by state/LGA
2. Report form: category, map pin, photo, description
3. Issue page: details, "me too" count, responsible authority
   contact card, share post generator
4. Browse: list of issues by state/LGA

## Core tables
- states (id, name)
- lgas (id, state_id, name)
- authorities (id, name, level [federal|state|lga], state_id, lga_id)
- contacts (id, authority_id, phone, email, x_handle, source_url,
  last_verified)
- issues (id, category, description, photo_url, location, lga_id,
  status, created_at)
- issue_votes (id, issue_id, voter_hash, created_at)

## Rules
- Contacts fall back: LGA, then state, then federal
- No accounts at first; limit reports per device/IP
- Never store or show personal data
- Neutral: show facts and numbers, not opinions

## Out of scope for MVP
Payments, native mobile app, government dashboards

as we develop and grow it keeps changing
