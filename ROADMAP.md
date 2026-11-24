# Member App — Feature Roadmap

**Status:** draft for discussion · updated 19 November 2026
**Scope:** features to add after the current mockup (workout plans and the in-gym experience), across the member app, the trainer app and the owner dashboard.

---

## Overview

We build the trainer and owner tools first, alongside the member app. The promise we sell is trainer-supervised coaching, and gym owners renew based on retention they can see. The member app alone delivers neither.

The product serves three people, and each needs their own surface:

- **Members** follow their plan, log workouts, track nutrition and progress, and call a coach for help.
- **Trainers** approve AI plans, answer floor requests, and follow up with members who need attention.
- **Owners** see engagement, at-risk members, trainer follow-through and renewals.

### How features are ranked

We sell to gyms, but members decide whether the app gets used. Every feature is scored on two kinds of value, plus effort.

- **Member value (1–5):** does it help members get results, or make them want to open the app?
- **Gym value (1–5):** does it help the gym keep members, earn more per member, or save trainer time? This is what makes gyms buy and renew.
- **Effort (S / M / L):** S is a few weeks for a small team, M is one to two months, L is a quarter or more, or needs new infrastructure or partners.

Priority weighs both value scores against effort, and accounts for dependencies.

| Priority | Meaning |
|----------|---------|
| **P0 · Now** | Build next. High value for members and gyms, or a foundation other features need. |
| **P1 · Next** | Strong value, but depends on a P0 feature or needs more build or partner work. |
| **P2 · Later** | Worth doing once the core is proven. Lower differentiation or high ongoing cost. |

---

## Summary

The roadmap has 22 features: 8 at P0, 10 at P1 and 4 at P2. One idea is not planned.

| # | Feature | Member value | Gym value | Effort | Priority | Phase |
|---|---------|:-:|:-:|:-:|:-:|:-:|
| 0 | Platform admin and gym onboarding | 1 | 5 | M | **P0** | 1 |
| 1 | Trainer app and console | 3 | 5 | M | **P0** | 1 |
| 2 | Owner dashboard and at-risk alerts | 3 | 5 | M | **P0** | 1 |
| 3 | Membership, check-in and renewals | 3 | 5 | M | **P0** | 1 |
| 4 | Offline mode for the gym floor | 4 | 3 | M | **P0** | 1 |
| 5 | Exercise video library | 4 | 4 | M | **P0** | 1 |
| 6 | Gamified progress | 4 | 5 | S–M | **P0** | 2 |
| 7 | Nutrition tracker | 5 | 4 | M | **P0** | 2 |
| 8 | WhatsApp integration | 4 | 4 | S–M | **P1** | 2 |
| 9 | Regional languages | 4 | 4 | M | **P1** | 2 |
| 10 | 4-week reassessment | 4 | 5 | S–M | **P1** | 2 |
| 11 | Injury and limitations profile | 4 | 4 | S | **P1** | 2 |
| 12 | Referrals | 2 | 4 | S | **P1** | 2 |
| 13 | AI food photo logging | 5 | 3 | L | **P1** | 3 |
| 14 | Products space (gym shop) | 3 | 5 | M–L | **P1** | 3 |
| 15 | QR codes on machines | 3 | 4 | S | **P1** | 3 |
| 16 | Home and travel workouts | 4 | 3 | S–M | **P1** | 3 |
| 17 | Wearable and health app sync | 3 | 2 | M | **P1** | 3 |
| 18 | Recipes | 3 | 2 | S–M | **P2** | 4 |
| 19 | Video and article space | 3 | 3 | M + ongoing | **P2** | 4 |
| 20 | Class booking | 3 | 4 | M | **P2** | 4 |
| 21 | Live gym crowd meter | 3 | 2 | M | **P2** | 4 |
| — | Food video logging | 2 | 1 | L | **Not planned** | — |

---

## P0 · Now

### 0. Platform admin and gym onboarding
**What:** an internal web console for our own team (dev, IT, ops), separate from the gym owner's console. We use it to take a new gym from lead to live. It captures the gym's basics, then provisions it as an isolated tenant and tracks setup until go-live.

**Why it matters:** every other feature assumes a gym already exists in the system. The PRD names a platform operator role and a provisioning endpoint (`POST /gyms`) but no screens for them. Without this, onboarding a gym means hand-editing the database.

**Scope v1:**
- **Gyms list:** every gym by stage (lead, onboarding, pilot, live, paused), with setup progress, AI spend and next step.
- **Onboarding wizard:**
  - gym and owner basics: brand and registered name, GSTIN, branch, address, hours, languages, owner contact, size
  - plan and pilot terms
  - branches and equipment
  - branding
  - review and provision
- **Agreement checks:** provisioning is blocked until the pilot agreement and data processing agreement are signed.
- **Go-live checklist:** trainers invited, equipment verified, gym QR printed, first members invited.
- **Support access:** time-bound and logged.

**Watch out for:** platform staff must never see member assessments, photos or chats (PRD role matrix). Paid prices stay "to be agreed" until D-01 is signed off.

**Measure:** days from signed pilot to go-live, and the share of onboarding steps done without engineering help.

**Mockup:** `App/Platform Admin.html` (OPS-01 to OPS-05).

### 1. Trainer app and console
**What:** a phone app for trainers on the floor and a web console for desk work. It holds a member list sorted by who needs attention, a plan approval queue, live "call a coach" requests, session feedback, form-check clips and member chat.

**Why it matters:** the member app already depends on trainer actions: approving plans, answering floor calls, reading feedback and reviewing the AI recap. None of those screens work without this. It is also how we deliver on "trainer-supervised", which is our main difference from consumer AI apps.

**Scope v1:** approval queue with edit and approve, a live request feed with accept and on-my-way, a member list with attention flags, chat.

**Depends on:** real-time messaging and push notifications.

**Watch out for:** trainers can't stare at a phone mid-session. Requests must be loud and one-tap: accept, then done.

**Measure:** median plan approval time, median response time to floor calls, share of calls answered.

### 2. Owner dashboard and at-risk alerts
**What:** AI flags members who have missed 2+ planned sessions, are trending down in attendance, or reported pain or "too hard". Their coach is prompted to reach out, and the app tracks whether they did. Owners see engagement, at-risk members, trainer follow-through and upcoming renewals.

**Why it matters:** this is the retention feature the product is built around: no member left unattended. It's also what owners judge when deciding whether to renew our subscription.

**Scope v1:** a weekly at-risk list per trainer, a suggested message the trainer can send in one tap, and an owner view of members flagged, contacted and returned.

**Depends on:** check-in data (#3) and workout logs.

**Watch out for:** alert fatigue. Cap flags per trainer per week and rank them, so the list stays actionable.

**Measure:** share of at-risk members contacted within 48 hours, share who return within 14 days, 90-day retention.

### 3. Membership, check-in and renewals
**What:** QR check-in at the front desk, membership status and expiry, UPI renewal in the app, renewal reminders, and freeze or pause requests.

**Why it matters:** this most directly pays for the product from the owner's side. It replaces registers and spreadsheets and recovers revenue lost to forgotten renewals. It also gives us the attendance data that powers streaks, at-risk alerts and the coach's view.

**Scope v1:** check-in QR, a status card on Profile, a UPI payment link for renewal, automatic reminders 7 days and 1 day before expiry.

**Depends on:** a payment gateway (Razorpay or Cashfree) and gym-side admin screens.

**Measure:** on-time renewal rate, share of renewals done in the app.

### 4. Offline mode for the gym floor
**What:** today's workout, the logger and the rest timer keep working with no signal, and sync later.

**Why it matters:** many Indian gyms are in basements or have poor reception. A logger that freezes mid-set is the fastest way to lose a member's trust. It's built into the logger from day one, because adding offline sync later is much harder.

**Scope v1:** cache the day's plan and demo videos, queue logged sets offline, sync on reconnect. Coach calls still need a connection, so the app shows that clearly.

**Measure:** sessions completed with at least one offline period, sync failures.

### 5. Exercise video library
**What:** a short looping demo for every exercise, shown in the logger, workout detail and swap sheet. Ideally recorded by the gym's own trainers on its own equipment, with a stock library as fallback.

**Why it matters:** members currently interrupt trainers to ask "how do I do this?". Demos cut those requests and keep form safe. Gym-recorded videos are also a branding win: our coaches, our machines.

**Scope v1:** a stock library of about 150 core exercises. Gyms can upload their own clip per exercise, guided by a recording template in the trainer app (angle, length, framing).

**Depends on:** video hosting and a CDN.

**Measure:** fewer form-check and call-coach requests per session, video plays per workout.

### 6. Gamified progress
**What:** builds on the streak and PRs already in the app. Adds badges (first PR, 10 workouts, 30-day streak), monthly gym-wide challenges, opt-in leaderboards inside the member's own gym, and streak protection on rest days.

**Why it matters:** gyms lose most members in the first three months, and streaks and challenges are the cheapest proven way to build a habit. Owners can run challenges as marketing, and leaderboards make the gym feel like a community, which consumer apps can't copy.

**Scope v1:** badges, gym challenges set up by the gym with optional real rewards (a free PT session, merchandise), seasonal challenges for New Year and festivals, and a weekly leaderboard by workouts completed.

**Depends on:** enough members at a gym using the app for leaderboards to feel alive, which is why it starts in phase 2.

**Watch out for:** leaderboards must be opt-in. Rank by consistency, not weight lifted, so beginners aren't discouraged.

**Measure:** 90-day member retention, workouts per member per week.

### 7. Nutrition tracker
**What:** daily calories and protein against targets set by the coach. A searchable food database with strong Indian coverage (dal, roti, idli, paneer, biryani, thali portions), and quick-add for repeat meals.

**Why it matters:** most members join to lose weight, and diet drives that result more than training. Coaches already give diet advice informally on WhatsApp. This brings it into the app, where the coach sees it next to the workout.

**Scope v1:**
- Manual logging with portions in katoris, rotis and pieces, not grams.
- A veg / egg / non-veg / Jain setting, and fasting days (Navratri, Ramadan).
- "Send my plate to my coach": a photo the coach can estimate and comment on. It needs no AI, and it builds a set of labelled Indian meal photos for #13.
- Protein and calorie rings on Home, and a coach view of the member's weekly average.

**Depends on:** licensing or building an Indian food database. Generic Western databases handle home-cooked Indian food badly. Sourcing starts in phase 1.

**Watch out for:** logging fatigue. Keep v1 to calories and protein only.

**Measure:** members logging food 4+ days a week, weight-goal progress for loggers vs non-loggers.

---

## P1 · Next

### 8. WhatsApp integration
**What:** workout reminders, renewal payment links, coach nudges, plan updates and the weekly recap, sent over WhatsApp.

**Why it matters:** Indian gyms already run on WhatsApp, and members read WhatsApp far more reliably than push notifications. It also reaches members who haven't installed the app yet.

**Scope v1:** templated messages for reminders, renewals and at-risk nudges (#2), each with a link back into the app.

**Depends on:** the WhatsApp Business API through a provider, and per-message costs priced into our plans.

**Watch out for:** spam. Members choose which message types they get, and we cap messages per week.

**Measure:** message open and click-through rates, returns after an at-risk nudge.

### 9. Regional languages
**What:** the full app in Hindi, Telugu, Tamil, Kannada, Marathi and others, chosen per member.

**Why it matters:** independent gyms in tier-2 and tier-3 cities are a large part of our market, and an English-only app limits who can use it. It's also a strong selling point when pitching to gyms.

**Scope v1:** UI, form cues and system messages in two languages to start, likely Hindi and Telugu given the Hyderabad pilot. Exercise names stay in English, with the regional script alongside, because that's how trainers say them on the floor.

### 10. 4-week reassessment
**What:** every 4 weeks, the member records measurements, progress photos and a short strength check. The coach reviews it and adjusts the plan. If the gym has a body-composition machine such as an InBody, the scan is imported here.

**Why it matters:** it closes the loop on progress, so members see results and don't drift. It's also the natural moment to offer a PT package, which feeds the products space (#14).

**Scope v1:** a reassessment reminder, a guided check-in flow, a coach review screen, and a before-and-after summary for the member.

**Measure:** share of members completing each reassessment, PT conversions after a reassessment.

### 11. Injury and limitations profile
**What:** onboarding asks about injuries and limitations. Plans avoid flagged movements, and the "I feel pain" button adds to the profile.

**Why it matters:** safety, and a strong selling point to gyms worried about liability. It also makes AI plans more trustworthy for trainers to approve.

**Scope v1:** a short injury checklist, exercise filters by joint, and pain reports visible to the coach.

**Watch out for:** we don't diagnose. The app flags and routes to the coach, and suggests a doctor for anything serious.

### 12. Referrals
**What:** "bring a friend": a free guest pass for the friend and a reward for the member.

**Why it matters:** gyms value cheap member acquisition, and it's quick to build once memberships (#3) exist.

**Measure:** guest passes redeemed, guests who join.

### 13. AI food photo logging
**What:** take a photo of a plate, and AI estimates the dish, portion and calories. The member confirms or edits it in one tap.

**Why it matters:** it's the biggest member delighter on this list, and it removes most of the logging effort that makes people quit nutrition tracking.

**Why not P0:** it needs the nutrition tracker and food database (#7) first. Accuracy on mixed Indian plates (thalis, curries, rice with sides) is hard, and poor accuracy at launch would hurt trust in the whole nutrition feature. The coach-reviewed photos from #7 give us training and test data.

**Scope v1:** photo, suggested dish and portion, member confirmation. Track how often members correct the estimate.

**Measure:** share of meals logged by photo, correction rate.

### 14. Products space (gym shop)
**What:** a branded in-app shop for the gym, with supplements, merchandise, PT packages and diet consultations, for pickup at the front desk or delivery.

**Why it matters:** a new revenue line for gyms, and a possible revenue share for us. PT packages are the highest-margin item for most gyms, and the app knows when a member might want one: a plateau, a new goal, a reassessment.

**Scope v1:** start with services (PT packages, consultations) and merchandise. Add supplements once compliance is sorted.

**Depends on:** payments (#3), stock management on the gym side, and supplement compliance (FSSAI labelling, no medical claims).

**Measure:** shop revenue per gym per month, PT package conversions.

### 15. QR codes on machines
**What:** a QR sticker on each machine. Scanning it shows the demo video, setup tips (seat height, pin position) and the member's last weights on that machine.

**Why it matters:** it makes "AI that knows your gym's equipment" something members can see and touch. It's cheap to do and hard for consumer apps to copy.

**Scope v1:** stickers generated from the gym's equipment list in the console, and a scan screen linking into the logger.

**Depends on:** the exercise video library (#5) and the gym's equipment setup in the trainer console (#1).

### 16. Home and travel workouts
**What:** a bodyweight or dumbbell version of the day's session for days a member can't reach the gym.

**Why it matters:** festivals, travel and exams are when members drift away. This keeps streaks and the habit alive through those gaps.

**Scope v1:** an "I can't make it today" option that swaps in a home version of the same muscle groups.

**Measure:** home sessions logged, members returning after a break.

### 17. Wearable and health app sync
**What:** read steps, heart rate, sleep and workouts from Apple Health, Google Health Connect and popular Indian fitness bands.

**Why it matters:** gives the coach and the AI a fuller picture (recovery, rest-day activity), and feeds rest-day streaks.

**Why P1:** useful, but only some members wear devices, and it doesn't help gyms sell.

---

## P2 · Later

### 18. Recipes
High-protein, budget-friendly Indian recipes (vegetarian first), linked to the member's nutrition targets, with one tap to log a recipe as a meal. Recipes are widely available elsewhere, so their value comes from the link to the nutrition tracker. Gym coaches could add their own recipes later.

### 19. Video and article space
A content feed of technique explainers, myth-busting, recovery and diet basics, where gyms can publish their own trainers' content. It drives engagement but needs ongoing content production that most independent gyms can't sustain. The exercise library (#5) covers the most-needed video first; revisit once a few gyms want to publish.

### 20. Class booking
Book group classes (Zumba, yoga, HIIT) with capacity limits and waitlists. High value for gyms that run classes and irrelevant for those that don't, so it's a toggle per gym.

### 21. Live gym crowd meter
Show how busy the gym is right now, so members can pick quieter times. It builds on the "machine is busy, swap exercise" idea. Check-ins (#3) only record arrivals, so it needs check-out scans or an estimated session length of about 75 minutes.

## Not planned

### Food video logging
Video adds little over a photo for estimating food, and costs far more to upload and process. Revisit only if photo logging (#13) shows that accuracy needs multiple angles.

---

## Suggested sequence

```
Phase 1 · Foundations       ─  Platform admin & gym onboarding (#0) · Trainer app and console (#1) · Owner dashboard and at-risk alerts (#2)
                               Membership and check-in (#3) · Offline mode (#4) · Exercise videos (#5)
                               Also: start sourcing the Indian food database

Phase 2 · Habits, nutrition ─  Gamified progress (#6) · Nutrition tracker (#7) · WhatsApp (#8)
                               Regional languages (#9) · 4-week reassessment (#10)
                               Injury profile (#11) · Referrals (#12)

Phase 3 · AI and revenue    ─  AI food photo logging (#13) · Products space (#14)
                               QR codes on machines (#15) · Home and travel workouts (#16) · Wearables (#17)

Phase 4 · Extras            ─  Recipes (#18) · Video and article space (#19) · Classes (#20) · Crowd meter (#21)
```

Phase 1 builds what the rest depends on: trainer and owner tools, memberships and a reliable logger. Phase 2 adds habit and nutrition features once members are active. Phase 3 brings the heavier AI and shop work. Phase 2 is the busiest, but four of its seven features are small.

---

## Measurement

Record a baseline at each pilot gym before launch. Without one, retention and attendance numbers have nothing to compare against.

**Baseline to capture (last 6 months, from gym records):**
- 90-day retention of new members
- Average visits per member per week
- On-time renewal rate
- Number of members per trainer

**Headline metrics after launch:**

| Metric | Who it matters to | Driven mainly by |
|--------|-------------------|------------------|
| 90-day member retention | Owner | #2, #6, #8 |
| Workouts per member per week | Owner, trainer | #6, #16 |
| At-risk members contacted within 48 hours | Owner | #1, #2 |
| Median response time to floor calls | Member, owner | #1 |
| On-time renewal rate | Owner | #3, #8 |
| Members logging food 4+ days a week | Member, trainer | #7, #13 |
| Shop and PT revenue per gym per month | Owner, us | #10, #14 |

---

## Open questions

1. Do we license an Indian food database or build our own? This decides when #7 and #13 can ship.
2. Which WhatsApp Business API provider do we use, and how do per-message costs fit into our pricing?
3. How do trainers receive floor calls mid-session: their own phone, a gym tablet, or a smartwatch?
4. What revenue share for the products space, and do gyms or we handle fulfilment?
5. Which two languages first? This depends on where the first paying gyms are.
6. Which body-composition machines are common in our target gyms, and can we import their data?
