# Feature Bank

Features we built or designed and then took out, changed, or held back, usually after stakeholder feedback. Each one keeps its screens and the reasoning behind it, so it can come back later without starting over.

- **Screens:**
  - [App/Feature Bank.html](App/Feature%20Bank.html) has parked features that would otherwise be lost. It includes a working prototype.
  - Older features still live in `App/Gym Companion.html`, `App/Platform Admin.html` or git history, linked below.
- **Figma:** parked screens go on the Exploration pages.

**Adding an entry.** When a feature is cut or changed:
1. Add an entry here with the date, who asked, and what they said.
2. Keep its screens. Either add a section to `App/Feature Bank.html`, or link to where they already live.
3. Never delete a working prototype.

Each entry covers the following.

| Field | What to write |
|---|---|
| **Status** | Parked / Replaced / Not built, with the date |
| **Screens** | Where the mockups live |
| **What it is** | One or two lines |
| **Why we built it** | The intent |
| **Why it changed** | Who decided, and their reason |
| **Thinking** | The rules and the choices behind them |
| **Rejected variants** | What was tried and dropped |
| **To bring it back** | What to decide or check first |

---

## Parked

### 1. Sets & reps tracking and in-workout adjustment · Gym Jodi

**Status:** Parked on 26 Nov 2026. It's still in `App/Gym Jodi.html` and will be removed in the next phase.

**Screens**

| Where | Frames |
|---|---|
| `App/Feature Bank.html`, section A | Prototype A0 and frames A1–A7 |
| `App/Gym Jodi.html` (until removed) | 22–25 and 34 |
| Figma, Gym Jodi page | 19–22 and 31. Move them to Exploration when the feature leaves the app |

**What it is**

Members record what actually happened on each set:
- **Couldn't complete** sits next to "Set N done" and opens a rep scroller. 0 means the set wasn't done.
- The remaining sets adjust on the spot.
- "How did it feel?" (Too easy / Just right / Hard) appears only after a fully completed exercise.

**Why we built it**

To collect as much as we can from each workout (reps per set and how each exercise felt) so Jod.ai's next 4-week plan fits the member better. The trainer sees the same data when approving the plan.

**Why it changed**

The manager felt it asks too much of members.

**Rules (built)**

| Situation | What happens |
|---|---|
| Missed by 1–2 reps | Same weight |
| Missed by 3 or more | Remaining sets about 10% lighter, shown as "35 kg · was 40" |
| 0 reps | The set shows "Not done"; remaining sets about 10% lighter |
| Weight steps | 1 kg up to 10 kg (dumbbells), 2.5 kg above |
| Undo | Restores the plan |

The code is `replan()` in Gym Jodi. A 0-rep save sets `skip: true`.

**Thinking behind the choices**

- **The member keeps going after a miss.** If you can't finish set 2, you don't walk away from the exercise; you do set 3 lighter. The user asked us to think like a trainer here. An earlier build blocked the rest of the exercise after a short set.
- **No feedback question after a short exercise.** The reps already show it was hard, so the screen moves straight on.
- **Orange marks only the short number** ("32/36"). Full reps are green ("36/36"), which gives the member something to chase. A screen full of orange after a hard day would feel like failing.
- **The label is "Couldn't complete", never "Fewer reps".** The user called "Fewer reps" stupid: this is an app talking, not two people. "Finish exercise early" was cut because it meant the same thing.
- **Undo is an explicit button.** Tapping a done set never un-marks it; the user called toggling "broken".
- **The sheet holds only the essentials:** "Set N · Exercise", the weight and the plan, the scroller (starting at plan − 1), and Save.
- **A certified coach or physio must review the rule table before launch.** Devpixel has no fitness staff.

**Make-up set (designed, not built)**

Problem: with 0 reps on a set, today's rule lowers the remaining sets, so the member does one set fewer (frame A4).

Requirement (user, 26 Nov): the member still completes every planned set.
- The 0-rep set stays in the list, disabled.
- A new card with the **same set number** appears directly below it, at the reduced weight.
- The remaining sets follow at that weight.

```
Set 1   40 kg     0/12        ← disabled
Set 1   32.5 kg   12 reps     ← added, now current
Set 2   32.5 kg   12 reps
Set 3   32.5 kg   12 reps
```

Proposed details, not confirmed yet:
- **Trigger:** only a 0-rep set gets a make-up. A partial set (1 rep or more) counts as a set.
- **Weight:** about 20% lighter, rounded to the plate step (40 → 32.5 kg). If someone gets no reps at 40 kg, 10% lighter (36 kg) usually fails too.
- **Second failure:** one make-up per exercise. Another 0-rep set ends the exercise, tells the trainer and skips the feedback question. Two total failures mean the plan weight is wrong, which needs a person, not further cuts.
- **Undo:** undoing the 0-rep set removes its make-up card, as long as the make-up isn't done yet.
- **Records:** the failed attempt stays in the log for Jod.ai and the trainer. Summaries count completed sets against the plan ("3/3 sets").

**Rejected variants**

- A number grid for entering reps.
- A copy of the onboarding weight ruler, with ticks. The user had meant that as an example of the interaction, not a spec.
- A live "Next set" preview inside the sheet.
- A red "Pain or discomfort" link in the sheet ("looks horrible"). Pain is reported from the ••• menu and the Trainer sheet.
- Tapping a set to toggle it between done and not done.

**To bring it back**

- Confirm the make-up set details.
- Decide whether "How did it feel?" stays in Gym Jodi once this goes. Its "only after a full exercise" rule depends on Couldn't complete.
- Get the coach/physio review.

---

## Replaced in Gym Jodi (screens kept in Gym Companion)

Gym Jodi replaced these. Their screens still work in `App/Gym Companion.html` (GC = its frame number).

| # | Feature | Replaced by | Why (who, when) | Screens |
|---|---|---|---|---|
| 2 | Logging weight and reps per set | Jod.ai sets every set, rep and weight; members tap a set when it's done | Jodi is for beginners, who shouldn't type weights and reps; they follow the plan (user, 25 Nov) | GC 17, 19 |
| 3 | Trainer approval for each swap | Instant swaps; the alternatives and their weights are approved with the plan | "Impractical and time wasting" (user, 25 Nov) | GC 21 |
| 4 | Progress photos | Body scans: a DEXA or InBody report, kept encrypted, visible to the member and their trainer | A major privacy issue, since even Devpixel staff could see members' photos. Documents are fine (user, 25 Nov) | GC 31 |
| 5 | QR check-in | Location check at Start workout (100 m), against the gym's Google Maps link from the admin | A QR check is difficult, and the admin already has the gym's exact location (user, 25 Nov) | GC 12 |
| 6 | Rest timer between sets; running workout clock | Timer only on cardio | A timer between sets "is not helpful, makes no sense" (user, 25 Nov) | GC 17 |
| 7 | Long onboarding: weight ruler, goal, experience & schedule, limits | 3 steps: Body (with body-scan upload), Goal & schedule, Health check | Less user fatigue; focus on goals and availability (user, 25 Nov) | GC 04–07 |
| 8 | Trainer fills in every weight (PRD rule) | Jod.ai sets the weights; the trainer approves the plan | Jodi decision (user, 25 Nov). Gym Companion keeps the PRD rule | GC 36 |

## Not in Gym Jodi yet

| # | Feature | Status | Screens |
|---|---|---|---|
| 9 | Trainer app pieces left out of Jodi's trainer app: Today queue with "needs attention" reasons, logging check-ins (attention coverage), transfer or escalate a request, filling in weights from a baseline test | Jodi's trainer app (26 Nov) covers the three jobs the user named: approve or rebuild plans, help requests, members. The rest can come later | GC 33, 34, 36, 38 |
| 10 | Owner console: attention dashboard, follow-ups, orientation, equipment, staff | Not redesigned for Jodi yet | GC 39–43 |

## Removed earlier (screens only in git history)

| # | Feature | Why | How to view |
|---|---|---|---|
| 11 | Trainers verify equipment; Draft states; member invites gated on 80% verified | Trainers have nothing to verify in their own gym, and half-done states leave gyms stuck. Our team now adds the full list in one go after a site visit (user, 24 Nov) | `git show 7c12734:"App/Gym Companion.html" > old.html` |
| 12 | Streaks and muscle recovery percentages (first mockup) | The PRD rules out recovery percentages and leaves out gamification. The muscle rings stayed, fed with logged sets | `git show c1f2756:"App/AI Gym App.html" > old.html` |

## Admin: after the pilot

| # | Feature | Where |
|---|---|---|
| 13 | Gym pipeline, detailed onboarding (legal and tax details, plans, agreements), provisioning | `App/Platform Admin.html`, frames L1–L5 |

The pilot admin shows these features locked: leads, plans and billing, legal and tax details, agreement tracking, multiple branches, usage, support access, ops team. Pricing stays out until PRD decision D-01 is signed off.

## Ideas, not built

| # | Idea | Notes |
|---|---|---|
| 14 | Equipment entry from the owner and trainer apps | Typed on the gym floor, with photos taken there |
| 15 | Roadmap features the PRD leaves out | Nutrition, gamification, payments/UPI renewals, WhatsApp, shop, referrals and more. See [ROADMAP.md](ROADMAP.md). Cut or deferred is still undecided |

The make-up set is part of #1.
