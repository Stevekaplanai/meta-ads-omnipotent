---
name: meta-ads-omnipotent
description: Complete Meta advertising mastery — how Meta's delivery stack actually works (Andromeda, GEM, Lattice, Sequence Learning, SUM, DLRM) fused with the operational audit framework (Pixel/CAPI health, creative diversity, account structure, audience) and the Andromeda-optimal build playbook. Use when auditing a Meta account, building or restructuring campaigns, diagnosing delivery or fatigue, planning creative volume, or advising a high-spend advertiser.
---

# Meta Ads Omnipotent

One skill, three layers that build on each other:

- **Part I — The Machine:** the six systems that decide whether an ad delivers at all.
- **Part II — The Audit:** the 50-check operational framework, scored and weighted, that finds where an account violates what Part I demands.
- **Part III — The Build:** the Andromeda-optimal structure to launch, scale, and refresh — what you do after the audit.

Never treat creative, targeting, bidding, or structure as isolated decisions. Every input has a downstream effect on retrieval, ranking, auction cost, and learning.

---

## PART I — THE MACHINE: Six Systems

### 1. Andromeda — Ad Retrieval Engine

Before any auction, Andromeda scans every active ad and selects ~1,000 candidates for a specific user at a specific moment. **If your ad doesn't pass retrieval, it never competes — no matter your bid.**

- Computer vision + AI audio analysis assign each creative an **Entity ID** from its visual pattern. Ads sharing a background, creator, or structure get the SAME Entity ID — thirty similar ads count as one retrieval ticket.
- **The 60% similarity rule:** Creative Similarity Score above 60% triggers retrieval suppression. Target a Diversity Index where active assets share fewer than 40% of visual/audio features. 100 minor variations perform no better than 10 genuinely distinct concepts.
- Runs on NVIDIA Grace Hopper + Meta MTIA hardware; 10,000x model capacity vs prior retrieval, 100x faster feature extraction. Global rollout completed October 2025, fully embedded by 2026.

**Implication:** creative diversity is a *delivery prerequisite*, not a performance variable. The first 3 seconds of video is scored by Andromeda's AI — the highest-leverage creative decision in the account.

### 2. GEM — Generative Ads Model (the central brain)

Meta's largest foundation model for recommendations, trained at LLM scale on the entire ecosystem (organic + paid, text/image/audio/video). It learns which creative styles work for which people and propagates that to every downstream model.

- Cross-surface personalisation at the individual level: a user who watches demos on Instagram but skips video in Feed gets video routed to Instagram automatically. No manual placement targeting needed.
- Measured impact: +5% conversions on Instagram, +3% on Facebook Feed (Q2 2025), doubled in Q3 2025; 4x more efficient than prior ranking models. GPUs training GEM doubled in Q4 2025.

**Implication:** the system knows what each person responds to before your campaign starts. It will override manual targeting based on creative signal. Your job is to feed GEM a wide, diverse creative signal set and let it route.

### 3. Lattice — Ranking & Auction Optimisation

A single multi-task, multi-domain ranking model replacing many siloed models. Ranks Andromeda's shortlist and determines auction value, learning across domains — built specifically to hold performance in a privacy-constrained, post-iOS-14 signal environment.

- Measured impact: +12% ad quality, +6% conversions, +10% top-line revenue metric, +11.5% user satisfaction, 20% infra capacity saved.

**Implication:** this is why broad targeting beats hyper-segmentation. Restricting the audience starves Lattice of data and worsens results.

### 4. Sequence Learning — User Journey Prediction

Reads user actions as a time-ordered sequence — order, frequency, timing, context — to predict the next action. The ski-trip example: after booking the resort, old DLRM kept showing resorts; Sequence Learning shows ski equipment, lift tickets, luggage. +2–4% conversions on select segments. GEM extends it: Meta optimises ad *sequences*, not individual ads.

**Implication:** funnel structure must mirror real journeys. Retargeting segments by journey position, not just "visited website." BOF creative speaks to the next action, never repeats the TOF message.

### 5. SUM — Scaling User Modelling

Upstream user models synthesise rich embeddings of each person — served via SOAP (latency-free, real-time) to hundreds of ranking models handling hundreds of billions of daily requests, so all models share one continuously updated understanding of every user.

**Implication:** Meta's model of your audience is richer than any manual interest stack. SUM is what makes broad targeting viable and usually superior.

### 6. DLRM — Conversion & Engagement Prediction

The foundational CTR/conversion-probability architecture (collaborative filtering + predictive analytics over sparse signals). Progressively succeeded by Sequence Learning and abstracted by GEM, but its principles still underpin prediction. Advantage+ campaigns on the full stack deliver $4.52 revenue per $1 spent — 22% above manually managed; 35% of US retail ad spend runs Advantage+.

**Implication:** every conversion signal you return via Pixel/CAPI trains this layer. Weak signal = the machine optimises toward the wrong people. Signal quality is a core performance input, not a technical nicety.

### How they chain

```
USER OPENS APP
  → ANDROMEDA   retrieval: ~1,000 candidates; low-diversity creative filtered out
  → SUM         user embedding pulled, fed to all downstream models
  → SEQUENCE    where is this user in their journey; what ad fits this moment
  → LATTICE     ranks candidates across objectives; picks auction entrants
  → DLRM        scores conversion probability × bid × estimated action rate
  → AUCTION     winner delivers
  → GEM         observes outcome, updates the whole stack
```

---

## PART II — THE AUDIT: 50 checks, weighted

Score every account 0–100 across four pillars. Evaluate each check PASS / WARNING / FAIL.

### Pixel / CAPI Health (30%) — feeds DLRM/GEM (Part I §6)

- Pixel installed and firing on all pages; correct currency + value parameters
- **CAPI active** (30–40% signal loss without it post-iOS 14.5); server events carry customer_information parameters
- Event deduplication configured (event_id matching, ≥90% dedup rate)
- **EMQ ≥8.0 on the Purchase/primary event**
- All standard events (ViewContent, AddToCart, Purchase, Lead) + custom conversions
- AEM configured for iOS; domain verified

**EMQ ladder:** 8.0–10.0 excellent (maintain) · 6.0–7.9 good (add parameters) · 4.0–5.9 fair (implement CAPI) · <4.0 poor (critical: CAPI + Enhanced Matching now). Parameters by match power: `em` (email) > `ph` (phone) > `fn`/`ln` > `ct`/`st`/`zp` > `external_id` (cross-device).

### Creative (30%) — feeds Andromeda retrieval (Part I §1)

- ≥3 formats active (image, video, carousel, collection); ≥5 creatives per ad set
- **Diversity Index: active assets share <40% of visual/audio features** (the Andromeda check — run it FIRST; failing it invalidates every other creative metric)
- Fatigue: CTR drop >20% over 14 days = FAIL; under Andromeda, conversion efficiency declines BEFORE CTR does — watch both
- Video: 15s max Stories/Reels, 30s max Feed; UGC/testimonial tested; DCO tested
- Copy: headline <40 chars, primary text <125 chars
- Refresh cadence: every 1–3 weeks at high spend (Andromeda accelerates fatigue by routing to the most responsive audience fast)
- **Never edit a live ad to refresh it — editing resets learning. Launch new.**

### Account Structure (20%) — feeds Lattice learning (Part I §3)

- Consolidation: 1–3 campaigns total; fewer, larger ad sets
- CBO vs ABO intentional; budget per ad set ≥5x target CPA (learning-phase exit minimum)
- Learning phase health: <30% of ad sets "Learning Limited" (FAIL >50%)
- Ad set audience overlap <30%; consistent naming; Advantage+ Sales active for e-commerce

### Audience & Targeting (20%) — respects SUM/Lattice (Part I §3, §5)

- Prospecting frequency (7-day) <3.0 (FAIL >5); retargeting <8.0 (FAIL >12)
- Custom Audiences (site, lists, engagement); Lookalikes tested at 1%/3%/5% seeds
- Advantage+ Audience tested vs manual; interests broad enough for the algorithm
- Purchasers excluded from prospecting; overlap managed; geo reviewed
- Manual targeting reserved for extreme niches or legally restricted categories only

### Special Ad Categories

Restricted verticals (credit, employment, housing, social issues — and financial products/services): declare the category before creation, verify targeting restrictions (no ZIP, 18–65+ only, no Lookalikes where barred), and screen creative against category policy. **For investment/financial advertisers this is the #1 account-disable vector — audit compliance before touching performance.**

### Key thresholds

| Metric | Pass | Warning | Fail |
|--------|------|---------|------|
| EMQ (primary event) | ≥8.0 | 6.0–7.9 | <6.0 |
| Dedup rate | ≥90% | 70–90% | <70% |
| CTR | ≥1.0% | 0.5–1.0% | <0.5% |
| Creative formats | ≥3 | 2 | 1 |
| Creatives per ad set | ≥5 | 3–4 | <3 |
| Learning Limited | <30% | 30–50% | >50% |
| Budget per ad set | ≥5x CPA | 2–5x CPA | <2x CPA |

### Audit output format

```
Meta Ads Health Score: XX/100 (Grade: X)
Pixel / CAPI Health: XX/100  (30%)
Creative:            XX/100  (30%)
Account Structure:   XX/100  (20%)
Audience:            XX/100  (20%)
```
Plus: full findings with pass/warning/fail, EMQ improvement roadmap, fatigue alerts, quick wins by impact, Advantage+ adoption recommendations.

---

## PART III — THE BUILD: Andromeda-optimal playbook

### Launch structure

- **1 campaign → 1–2 ad sets → 10–20 genuinely diverse creatives.** One place for the algorithm to learn; CBO on top so Lattice allocates dynamically.
- Broad / Advantage+ audience by default. Creative IS the targeting: each distinct concept recruits its own audience through Andromeda retrieval.
- CAPI live before the first dollar. Signal from day one is what shortens learning.

### Creative production system

- Plan volume around **distinct concepts, not variations**: different creators, backgrounds, formats, hooks, angles — each earning its own Entity ID.
- Formats that outperform in GEM's training data: video, UGC-style, mobile-native over polished production.
- Hook (first 3 seconds) gets the most iteration — it is scored at retrieval.
- Refresh cycle 1–3 weeks at high spend. Pause fatigued ads (conversion efficiency declining) before they drag campaign learning; replace with NEW ads, never edits.

### Scaling rules

- Raise budgets ≤20–30% per move; sharp changes disrupt learning.
- Scale by adding diverse creative concepts, not by cloning campaigns — fragmentation splits signal.
- Journey-based retargeting per Sequence Learning: segment by position (viewed → engaged → initiated → purchased) and speak to the NEXT action.

### What the algorithm rewards / penalises

| Rewards | Penalises |
|---|---|
| Creative diversity across formats, hooks, styles | High creative similarity (shared Entity IDs) |
| Clean high-volume CAPI signal | Missing/weak conversion signal |
| Broad audiences with room to optimise | Over-constrained audiences |
| Stable structure, stable spend | Frequent edits resetting learning; sharp budget swings |
| Consolidated campaigns | Fragmented structure, small scattered budgets |

### Diagnostic questions for any account

1. **Retrieval health:** are active creatives diverse enough to pass Andromeda? Similarity score?
2. **Signal quality:** CAPI live? Events firing? Match rate?
3. **Fatigue:** frequency per ad per week? Conversion efficiency declining while CTR looks "normal"?
4. **Structure:** how many campaigns/ad sets/ads? Budget fragmented?
5. **Journey mapping:** do retargeting audiences reflect Sequence Learning position?
6. **Refresh:** any creative older than 3 weeks at high spend?
7. **Stability:** sharp budget changes in the last 7 days?
8. **Compliance:** correct Special Ad Category declared; creative screened against vertical policy? (For financial advertisers, run this FIRST.)

### Emerging: Threads placement

GA Jan 2026, 400M+ MAU, lower CPMs than Feed/Stories, ~0.04% of spend today. Enable within Advantage+ Placements; monitor CPM/engagement; early-mover advantage if the brand runs an active Threads presence.

---

## Sources

- [Meta Engineering: Andromeda](https://engineering.fb.com/2024/12/02/production-engineering/meta-andromeda-advantage-automation-next-gen-personalized-ads-retrieval-engine/)
- [Meta Engineering: GEM](https://engineering.fb.com/2025/11/10/ml-applications/metas-generative-ads-model-gem-the-central-brain-accelerating-ads-recommendation-ai-innovation/)
- [Meta Engineering: Sequence Learning](https://engineering.fb.com/2024/11/19/data-infrastructure/sequence-learning-personalized-ads-recommendations/)
- [Meta AI: Lattice](https://ai.meta.com/blog/ai-ads-performance-efficiency-meta-lattice/)
- [Meta AI: DLRM](https://ai.meta.com/blog/dlrm-an-advanced-open-source-deep-learning-recommendation-model/)
- [arXiv: SUM — Scaling User Modelling](https://arxiv.org/abs/2311.09544)
- [Meta for Business: AI Innovation in Ads Ranking](https://www.facebook.com/business/news/ai-innovation-in-metas-ads-ranking-driving-advertiser-performance)
- [Search Engine Land: Andromeda + GEM](https://searchengineland.com/meta-ai-driven-advertising-system-andromeda-gem-468020)

Operational audit framework adapted from the claude-ads `ads-meta` skill (AgriciDaniel/claude-ads).
