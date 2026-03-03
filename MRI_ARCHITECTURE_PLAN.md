# MRI Remittance System - Architecture & Strategy Plan

## Executive Summary
**Goal:** Build MVP for 1,000 CIF test batch before Ramadhan/Hari Raya
**Revenue Target:** RM4/transaction
**Timeline:** 2 weeks for MVP

---

## 1. WhatsApp Bot - Cost-Effective Solution 💰

### Problem: WhatsApp Business API is expensive
- **Official API:** $0.005-0.09 per message (Meta/Facebook)
- **360dialog:** ~$0.005 per message + monthly fee
- **For 1,000 customers:** Could be $50-100 just for initial outreach

### Solution: Hybrid Approach (FREE + PAID)

**Phase 1: FREE WhatsApp Web Automation**
- Use **whatsapp-web.js** (Node.js library)
- Connect to WhatsApp Web via QR code
- **Cost:** FREE (uses your phone's WhatsApp)
- **Limitation:** ~100 messages/hour rate limit, not for production scale
- **Good for:** Testing with 1,000 CIF batch

**Phase 2: Affordable API (When scaling)**
- **WATI.io** - $39/month unlimited messages (best value)
- **ChatAPI** - $39/month for 10,000 messages
- **Switch to official API** when revenue justifies it

### WhatsApp Bot Flow (Based on Your Dashboard)

```
1. OUTREACH (Initial)
   Bot: "Halo Kak {{nama}}! Kami dari Mandiri International Remittance..."
   
2. USER RESPONDS "YA"
   Bot: "Terima kasih! Sila hantar butiran penerima di Indonesia..."
   
3. COLLECT INFO
   Bot guides through:
   - Nama penerima
   - No. akaun bank
   - Nama bank (BRI/BCA/Mandiri/BNI)
   - Hubungan
   
4. CONFIRM AMOUNT
   Bot: "Berapa RM nak hantar? Rate hari ini: 1 MYR = 3,250 IDR"
   
5. GENERATE REF
   Bot: "Terima kasih! Ref: MIR-2025-XXXXXX"
   
6. AWAIT SLIP
   Bot: "Sila bank in ke akaun MRI dan hantar slip disini"
```

---

## 2. Tech Stack Recommendations

### Core Platform
| Component | Technology | Reason |
|-----------|------------|--------|
| **Dashboard** | Next.js + your existing Command Center | Reuse components, faster |
| **Database** | PostgreSQL (Neon or Supabase) | Free tier, scalable |
| **WhatsApp Bot** | whatsapp-web.js (Phase 1) | FREE for testing |
| **PDF OCR** | Tesseract.js (client-side) or Python + Tesseract | Extract CIF data from MRI PDFs |
| **Hosting** | Vercel (dashboard) + Railway/Render (bot) | Free tiers |

### FREE Tier Limits (Good for 1,000 CIF test)
- **Vercel:** Free forever for frontend
- **Neon PostgreSQL:** 500MB, 190 compute hours/month
- **Railway:** $5 free credit/month (enough for bot)
- **whatsapp-web.js:** FREE (uses your phone)

---

## 3. Social Media Marketing Strategy

### Target Audience Analysis
**Indonesian Workers in Malaysia:**
- Age: 20-45 years old
- Occupation: Factory workers, cleaners, construction
- Income: RM 1,500-3,500/month
- Phone usage: Heavy TikTok, Facebook, WhatsApp

### Platform Priority (Based on Research)

| Platform | Usage Among Target | Recommendation |
|----------|-------------------|----------------|
| **TikTok** | 🔥🔥🔥 VERY HIGH | #1 Priority - Short videos, viral potential |
| **Facebook** | 🔥🔥 HIGH | #2 Priority - Groups, older demographic |
| **WhatsApp** | 🔥🔥🔥 VERY HIGH | Bot outreach + status updates |
| **Instagram** | 🔥 MEDIUM | Lower priority - more urban audience |

### Content Strategy for TikTok (Recommended)

**Video Ideas:**
1. **"Cara kirim duit ke Indonesia guna MRI"** (How to send money)
   - 15-30 sec tutorial
   - Show phone screen recording
   - Malay + Indonesian language

2. **Testimonials**
   - "Kak Siti hantar RM500, duit sampai dalam 1 hari!"
   - Real user stories

3. **Rate Comparisons**
   - "Jangan tukar di kedai! Guna MRI lebih untung"
   - Visual comparison

4. **Ramadhan Special**
   - "Kirim duit THR untuk keluarga di Indonesia"
   - Emotional appeal

**Hashtags:**
- #TKI (Tenaga Kerja Indonesia)
- #PekerjaIndonesia
- #KirimUang
- #Remittance
- #Ramadhan2026
- #HariRaya

---

## 4. Implementation Timeline (2-Week MVP)

### Week 1: Foundation

**Day 1-2: Database & API**
- [ ] Set up PostgreSQL (Neon)
- [ ] Create tables: customers, transactions, references
- [ ] Build API endpoints for CRUD

**Day 3-4: PDF OCR Pipeline**
- [ ] Set up Tesseract for PDF text extraction
- [ ] Parse MRI CIF format (name, IC, phone, employer)
- [ ] Import 1,000 CIF test batch

**Day 5-7: WhatsApp Bot (Basic)**
- [ ] Set up whatsapp-web.js
- [ ] Create message templates (Bahasa Indonesia)
- [ ] Build conversation flow (outreach → collect info → generate ref)
- [ ] Test with 10-20 real customers

### Week 2: Dashboard & Integration

**Day 8-10: Admin Dashboard**
- [ ] Adapt your draft dashboard to Next.js
- [ ] Connect to API
- [ ] Live transaction feed
- [ ] Reference number generator

**Day 11-12: MRI Integration**
- [ ] Build forward-to-MRI system
- [ ] WhatsApp message formatter (to send to MRI agents)
- [ ] Commission tracking

**Day 13-14: Testing & Launch**
- [ ] End-to-end testing
- [ ] Train MRI team
- [ ] Launch to 1,000 CIF batch

---

## 5. Customer Journey (Based on Your Dashboard)

```
┌─────────────────────────────────────────────────────────────┐
│  MRI INTERNAL                                               │
│  Export CIF PDF → OCR Extract → Import to Database          │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│  BINA DIGITAL PLATFORM                                      │
│                                                             │
│  1. 📤 WhatsApp Bot Outreach                                 │
│     "Halo Kak! Mau kirim duit ke Indonesia?"                │
│                                                             │
│  2. 💬 Customer Response                                     │
│     Customer: "YA, mau!"                                    │
│                                                             │
│  3. 📝 Collect Info                                          │
│     Bot guides: Penerima, Bank, Akaun, Jumlah               │
│                                                             │
│  4. 🎫 Generate Reference                                    │
│     MIR-2025-001847                                         │
│                                                             │
│  5. ⏳ Await Transfer Slip                                   │
│     Customer sends bank slip via WhatsApp                   │
│                                                             │
│  6. 🏦 Forward to MRI                                        │
│     Auto-format WhatsApp message to MRI agent               │
│                                                             │
│  7. ✅ Transaction Complete                                  │
│     Track status, update dashboard                          │
│                                                             │
│  8. 💰 Commission Tracked                                    │
│     RM4 per transaction recorded                            │
└─────────────────────────────────────────────────────────────┘
```

---

## 6. Ramadhan/Hari Raya Campaign Strategy

### Timing (Critical!)
- **Ramadhan 2026:** Expected March-April
- **Hari Raya:** Expected early April
- **Target Launch:** 2 weeks before Ramadhan starts

### Campaign Ideas

**1. "THR Express" (Tunjangan Hari Raya)**
- Target: Workers sending Raya bonus home
- Message: "Kirim THR untuk keluarga, sampai sebelum Raya!"
- Timing: 2-3 weeks before Raya

**2. "Ramadhan Special Rate"**
- Slightly better rate (if MRI allows)
- Marketing: "Rate istimewa Ramadhan!"

**3. "Puasa Challenge" Social Media**
- TikTok challenge: "Show your Raya preparation"
- Prize: Free transaction fee
- Viral potential

---

## 7. Risk Mitigation

| Risk | Mitigation |
|------|------------|
| WhatsApp bans | Use personal WhatsApp initially, migrate to official API when scaled |
| PDF OCR errors | Manual review for first 100, improve regex patterns |
| MRI delays | Set expectation: 1-2 business days |
| Low response rate | A/B test message templates, follow-up sequence |
| Legal compliance | Ensure MRI handles KYC, we just facilitate |

---

## 8. Success Metrics (1,000 CIF Test)

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Outreach sent** | 1,000 | WhatsApp messages delivered |
| **Response rate** | 30% | Customers who reply |
| **Conversion rate** | 10% | Completed transactions |
| **Transactions** | 100 | In 2-week test period |
| **Revenue** | RM 400 | 100 × RM4 |
| **If successful** | Scale to 20,000 | Next batch |

---

## Next Steps

**Ready to build? I recommend:**

1. **Spawn Samantha** → Build database + API foundation
2. **Spawn Mason** → Set up WhatsApp bot infrastructure  
3. **Spawn Ellie** → Polish dashboard UI based on your draft
4. **Spawn Priya** → Create TikTok marketing strategy & content plan
5. **Spawn Dylan** → Write user manual for MRI team

**Your call, Syed. Which should we start with?**
