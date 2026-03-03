# MRI Production

Canonical source-of-truth for MRI remittance system.

## Structure
- `web/` — Next.js web app (admin dashboard + ops UI)
- `MRI_ARCHITECTURE_PLAN.md` — legacy architecture notes
- `MRI_EMERGENCY_PLAN.md` — emergency launch plan notes
- `MRI_LAUNCH_SUMMARY.md` — launch summary notes

## Local Development
```bash
cd web
npm install
npm run dev
```

Default local URL: `http://localhost:3000`

## Deployment
- GitHub repo: `bina-digital/mri-production`
- Vercel project: `mri-production`

## Immediate Priorities
1. Contract-to-requirements extraction
2. Data model finalization (customers, transactions, payout workflow)
3. WhatsApp intake + reference generation flow
4. Admin queue and status lifecycle
5. Production hardening (auth, audit logs, env secrets)
