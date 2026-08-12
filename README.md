# ReliefLink — Camp Portal

Camp coordinator portal for **Relief Camp Resource Coordinator**, a live
platform that connects flood relief camps with donors in real time.

This app lets camp coordinators register relief camps and post/update the
resources they need (blankets, drinking water, medicine, etc.), so donors and
the public dashboard can see needs the moment they're posted.

**Live app:** https://relieflink-camp-portal.vercel.app
**Donor Portal (companion app):** https://camp-donor-portal.vercel.app

## What it does

- Register a relief camp (name, state, district, location, contact)
- Post urgent resource requirements with quantity and urgency
- Track fulfillment live as donors claim resources — no manual updates
- PIN-gated access for camp coordinators

## Tech stack

- **React + Vite + TypeScript** — frontend
- **Tailwind CSS** — styling
- **Supabase** — database (PostgreSQL), real-time sync, and backend logic

## Data model

Backed by three tables: `camps` → `needs` → `claims`. A need's
`quantity_fulfilled` and `status` are never edited directly — they're
derived automatically from donor claims via a backend function, so the
numbers can't drift out of sync.

## Run locally

**Prerequisites:** Node.js (v18+)

\`\`\`bash
npm install
\`\`\`

Create a `.env` file with your Supabase project credentials:

\`\`\`
VITE_SUPABASE_URL=your-supabase-project-url
VITE_SUPABASE_ANON_KEY=your-supabase-publishable-key
VITE_DONOR_PORTAL_URL=https://camp-donor-portal.vercel.app
\`\`\`

\`\`\`bash
npm run dev
\`\`\`

Open the printed `localhost` URL and enter the access PIN (`1234`) to enter
the Camp Portal.

## Notes

- `quantity_fulfilled` and `status` on a need are backend-controlled —
  don't add UI that edits these fields directly.
- `urgency` only accepts: `critical`, `high`, `moderate`.

---

Built for a hackathon by **Scout Regiment**.
