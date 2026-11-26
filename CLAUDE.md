# CLAUDE.md: shared context for this repo

We work on this repo from different Claude accounts, so nothing carries over between sessions except what is written here. Read this file and `README.md` before changing anything.

**Keep it current.** When the user makes a product decision, settles an open question or plans a feature, update this file in the same turn. Add the date and the reason.

---

## 1. What this repo is

HTML mockups and prototypes for a B2B gym platform for independent gyms in India. An AI builds each member's workout plan from the gym's equipment, a trainer approves it, and the member follows it on the gym floor with a trainer on call. Devpixel builds it; the user is the product designer and owns v1 product decisions.

| File | What it is | Status |
|---|---|---|
| `App/Gym Jodi.html` | Beginner member app plus its trainer app: 56 frames (42 member, 14 trainer) and one prototype phone that switches between the two | **Current app.** Most work happens here |
| `App/Platform Admin Pilot.html` | Our team's console for onboarding gyms: prototype, developer rules, 10 frames | **Build now** (pilot) |
| `App/Platform Admin.html` | Full admin for after the pilot | Reference only |
| `App/Gym Companion.html` | Earlier member, trainer and owner app, built to the PRD | Previous version (Exploration in Figma) |
| `FEATURE-BANK.md` + `App/Feature Bank.html` | Features we built and then cut or changed: the reasoning, plus screens and a working prototype | Add to it whenever a feature is cut (§2, rule 10) |
| `ROADMAP.md`, `Roadmap Presentation.html` | Feature roadmap from 19 Nov 2026 (P0–P2) | Older than the PRD; see §6 |

**Figma:** file `Ymy4LJVsha2qGaSKvsyq3D` ("Gym"), described in §8.

**Sample data** is the same everywhere: member Arjun Reddy, Coach Ravi Kumar, Iron Temple Gym, Banjara Hills, Hyderabad, Thu 19 Nov. The admin user is Nikhil.

### Gym Companion vs Gym Jodi: different rules

- **Gym Companion** follows the manager's PRD (*Gym Companion PRD v1.0*, a PDF from the Director of Engineering, 23 Nov 2026; not in the repo):
  - the trainer sets every weight
  - swaps wait for trainer approval
  - progress photos
  - the old red #FF5A5F
- **Gym Jodi** follows the user's later decisions (§3). **Jod.ai builds the plan, including every set, rep and weight; the trainer only approves it.**
  - Never write that the trainer sets weights in Jodi. Getting this wrong made the user angry (25 Nov 2026).
- Gym Companion has **not** been updated to match Jodi. Ask before porting anything across.

---

## 2. How to work with the user

These rules came from corrections. Breaking one costs a round trip and the user's trust.

1. **Discussion is not a build request.** If the user is asking, thinking aloud or says "just discussing", answer and recommend; don't edit files.
2. **No silent removals.** Never remove or move an existing feature as part of a larger change. Ask a separate, plain question ("Remove X?" / "Move X to Y?") and wait for a yes. When unsure, leave it where it is.
   - Example: How to and Swap were once moved into a ••• menu as one item of a "cleanup" list. The user was angry.
3. **Practical v1 beats the PRD.** The PRD is the manager's starting point. For each rule, ask:
   - Who does this step in real life?
   - Is it needed?
   - What happens if it's left half done?

   Cut steps that add nothing; keep the safety intent (pain holds, honest help status). When we deviate from the PRD, write it in `README.md` so the Director of Engineering sees it.
4. **Terse UI copy.** Screens show labels, data and actions only.
   - No sentences explaining rules.
   - No "we" or "our team".
   - No PRD references on screen.
   - No obvious qualifiers (e.g. "Optional · self-reported" was replaced by a **Log weight** button).

   Page titles are nouns and buttons are verbs. Rationale goes in README or frame hints, never on screen.
5. **Plain facts, not targets.** Show counts and dates ("3 · 2 live, 1 setting up"), not program goals ("3 of 3 · target reached", "Day 11 of 45").
   - Design every list and summary for **4, 40 and 400 rows**. Summary boxes never name individual items. A cell that holds several items shows the first, then +N.
6. **Keep rich visuals.** If a graphic breaks a rule, feed it honest data rather than deleting it.
   - Example: the muscle rings now show the share of today's sets.
7. **Self-review before replying.** Screenshot every affected frame in both themes and check:
   - alignment and spacing
   - consistent casing ("optional" is lowercase)
   - meaningless fields
   - real-world logic

   Fix everything in the same turn. A user's example ("like the weight scale") is inspiration, not a spec to clone.
8. **Summaries name the experience changes** (e.g. "onboarding now has the DEXA upload step"), not internal refactors.
9. **Git:** commit or push only when asked. Use descriptive messages. Work on `main`.
10. **Never trash a feature.** Features often get cut or changed after stakeholder feedback. When that happens:
    - Record it in `FEATURE-BANK.md`: what it is, why we built it, who changed it and why, the thinking and rules, rejected variants, and what to decide before bringing it back.
    - Keep its screens. Add a section to `App/Feature Bank.html` (prototype included), or link to where they already live.
    - In Figma, move its screens to Exploration.
    - Do this before removing anything from the live file.

---

## 3. Gym Jodi: decisions and why

`README.md` → "Gym Jodi" lists what the screens do. This section adds who decided what, and why.

- **Who it's for:** beginners. Strip anything that doesn't help them.
- **Plan ownership (25 Nov):**
  - Jod.ai builds the plan on day one and restructures it every 4 weeks from progress and feedback.
  - The trainer approves each version.
  - Members never type weights or reps. Weights can differ per set.
- **Sets:** the screen shows the current set large and lists every set.
  - Tap a set to mark it done. Undo is an explicit, small grey button; tapping a done set never toggles it (the user called toggling "broken").
  - The current set has a green tint, with no badge or border.
- **Couldn't complete** (never "Fewer reps") opens a sheet with exactly these items:
  - "Set N · Exercise", the weight and the plan
  - an Apple-style number scroller: the lens is large, neighbours fade, it starts at plan − 1, and 0 means not done
  - Save
- **Rejected for the Couldn't complete sheet:**
  - a number grid
  - a copy of the onboarding ruler
  - a live "next set" preview
  - a red pain link ("looks horrible")
- **Where pain is reported:** the ••• menu (Report pain) and the Trainer sheet.
- **Adjustment rule today:**
  - missed by 1–2 reps → keep the weight
  - missed by 3 or more, or 0 reps → the remaining sets are about 10% lighter (1 kg steps up to 10 kg, 2.5 kg above)
  - The whole sets & reps feature is parked (§4).
- **Feedback:** Too easy / Just right / Hard. It's asked only after an exercise is fully completed. If any set was short, or cardio stopped early, the app moves straight on.
- **Rep colours:**
  - orange for short reps ("32/36")
  - green for full reps ("36/36"), so there's something to chase
  - weights and feelings stay neutral
- **Red is for pain only:** #E5534B dark, #CF222E light, used as an accent. Hold boxes are neutral cards with a red icon. The user disliked the old pink-red and the "too red" pain screens.
- **Exercise card action row:** How to · Swap · Trainer.
  - Trainer is the accent item with a ripple and shows the live request status.
  - There's no floating button; it crowded the ••• button.
  - Report pain and Finish workout are in the ••• menu. The user wants to rethink both (§5).
- **Timers:** no rest timer ("pointless") and no running workout clock. The only timer is the countdown on cardio exercises.
- **Instant swaps (25 Nov):** trainer approval per swap was "impractical and time wasting".
  - The alternatives and their weights are approved with the plan.
  - "Back to …" restores the original.
  - Swaps lock once a set is done or the cardio timer starts.
- **Start workout checks location; there's no QR check-in:**
  - The gym's location comes from a Google Maps link in the admin.
  - The phone is checked once, at Start workout, against a 100 m radius. There's no background tracking.
  - Outside the radius, the app asks "Are you at [gym]?":
    - Yes counts the visit and logs a location mismatch.
    - No means it isn't a visit, and trainer help is hidden.
- **Body scans instead of photos (25 Nov):** photos were a privacy problem, since even our team could see them.
  - Members upload a DEXA or InBody report as a PDF or photo.
  - The file is kept encrypted and visible only to the member and their trainer.
  - Documents are fine; only body photos were the concern.
- **Onboarding has 3 steps:**
  1. Body: one screen with Upload body scan, Height & weight, and optional Body composition. The user called separate scan and manual screens pointless.
  2. Goal & schedule: goal, experience, days per week, session length, and diet as one tap (Veg / Eggetarian / Non-veg / Vegan).
  3. Health check: the severe-symptom hold stays.
- **Sign in (26 Nov):** phone number (+91) → 6-digit code. Three outcomes:
  - a new number with an invite → Invite & verify
  - a member's number → Home
  - an unknown number → "This number isn't linked to a gym"
- **Before launch:** a certified coach or physio must review every rule table. Devpixel has no fitness staff.

### Gym Jodi trainer app (26 Nov 2026, frames 43–56)

The user named the trainer's main jobs for this iteration:
1. Approve AI plans. If the trainer doesn't approve, they give instructions and inputs, and the AI redoes the plan.
2. Help requests, such as spotting.
3. A list of all members, to check their info.

They hadn't fully reviewed the Gym Companion trainer screens. Build on these three and ask before adding more.

- **Plans:** the trainer still never types a weight.
  - Per exercise, the inputs are Lighter / Heavier / Fewer reps / More reps (Shorter / Longer for cardio), Replace with an approved alternative, plus an optional note.
  - The instructions are free text, sent together with the inputs.
  - Once any exercise has a change, Approve gives way to "Request changes · N".
  - Jod.ai rebuilds the plan (the prototype takes about 2.6 s, deterministic). The next version shows "Changes from v1" with "was" values and the notes quoted.
  - Approving applies the new version to the member's workouts. The member sees "Being updated" while Jod.ai works.
- **Help:**
  - The trainer sees their own open requests and those another trainer accepted.
  - Accept, On my way and Resolve update the member's phone.
  - Pain outcomes: Cleared in person (lifts the hold), Keep on hold today, Advised medical help.
- **Members:**
  - Every member of the gym, not just the trainer's own. There's a Mine filter.
  - Search and filters, with counts derived from the list.
  - The member record covers the profile, plan, body scans with report files, workouts and help history.
- **Not carried over from Gym Companion's trainer app:** Today queue, check-in logging (attention coverage), transfer/escalate. See `FEATURE-BANK.md` #9.
- **Prototype limits:** only Arjun's rows open; the other members are sample rows.

---

## 4. Sets & reps tracking is parked

**Parked on 26 Nov 2026.** This covers Couldn't complete, the rep scroller, in-workout weight adjustment and feedback only after a full exercise.
- **Why it was built:** the user wanted to collect as much data as possible from each workout, to improve Jod.ai's plans.
- **Why it was parked:** the manager felt it asks too much of members.

**What happens next**
- It stays in `App/Gym Jodi.html` until the next phase. The user will ask for the removal; don't remove it unprompted.
- The full record is in `FEATURE-BANK.md` #1: the rules, the thinking, rejected variants, and the make-up set design that was never built.
- The screens and a working prototype are in `App/Feature Bank.html`, section A.

---

## 5. Open questions

| Question | Context |
|---|---|
| Make-up set details | Only if sets & reps tracking comes back. `FEATURE-BANK.md` #1 |
| Does "How did it feel?" stay once sets & reps tracking leaves Gym Jodi? | Its "only after a full exercise" rule depends on Couldn't complete |
| Can the plan change weights between the 4-week reviews? | Plan v2 says "leg press up to 40 kg, after your feedback", and the weekly chat summary says "so it goes up to 40 kg". Both imply mid-cycle changes, which conflicts with Jod.ai restructuring only every 4 weeks. Also noted on the Figma Read me page |
| Admin sign-in method | Email + code (built) or Google Workspace sign-in |
| App logo | Placeholder: an accent tile with a dumbbell |
| Admin input focus colour | HTML uses the orange accent ring; Figma uses green. Ask before syncing |
| Port Jodi changes to Gym Companion? | Instant swaps, no photos, the calmer red |
| Finish workout flow and ••• menu | The user wants to rethink both |
| PRD gaps: cut or deferred? | The PRD leaves out nutrition, gamification, payments/UPI renewals, WhatsApp, shop and referrals, which were P0/P1 in `ROADMAP.md`. The mockups leave them out |
| Pricing | Stays out until PRD decision D-01 is signed off |
| Who can open a member's body scan reports? | Earlier rule: the member and *their* trainer. The trainer app lists every member, so decide whether any trainer on shift can open reports, or only the assigned one |
| Can a trainer ask Jod.ai for changes between 4-week updates? | Not built (the member record only has View plan). Ties to the plan-weight question above |
| Trainer chat on the trainer side | Members have a Trainer chat tab; the trainer app has no chat or Message button yet |

---

## 6. Planned and maybe

**Planned**
- **Next phase: remove sets & reps tracking from Gym Jodi** (the user's plan, 26 Nov; wait for them to ask).
  - Screens and prototype are already kept in `App/Feature Bank.html`.
  - In Figma, Gym Jodi frames 19–22 and 31 move to Exploration.
- Coach/physio review of the rule tables before launch.
- Figma sync for the sign-in screens:
  - 3 mobile screens; Jodi HTML frames are numbered 3 higher than Figma
  - 2 admin screens; admin HTML is 2 higher
  - The Gym Jodi trainer app (frames 43–56) isn't in Figma either
  - The user said "no need right away".
- Icons: we use **Lucide** (open source, ISC licence, 24 px grid, 1.75 stroke), plus custom icons for the dumbbell and filled play/pause. The user will add the Lucide library to Figma by hand.

**Maybe / later**
- Equipment entry from the owner and trainer apps (typed on the gym floor, photos taken there).
- After-pilot admin features: leads, plans and billing, legal and tax details, agreements, multiple branches, usage, support access, ops team. They are shown locked in the pilot file.

**Engineering notes**
- Encrypt scan files at rest; build no admin or support view of them.
- Resolve short `maps.app.goo.gl` links on the server.
- Engineering supplies the equipment catalog (name, type, default weights, aliases). Don't build "all machines in the world" data.

**Admin pilot rules**
- Our team sets up gyms in one go after a site visit.
- Trainers don't verify equipment.
- There are no partial "3 of 12" states.
- Don't add fields to Add a gym without the user's say-so.

---

## 7. Building and checking the HTML files

The HTML files are design references, not production code; developers choose their own structure. Each file in `App/` is self-contained, with no build step, and it's the source of truth. Edit it directly.

`App/Feature Bank.html` is a frozen copy of the Gym Jodi code from 26 Nov 2026, with its own canvas. To park another Jodi feature, add a section, and frames whose state shows it, to that file's canvas script at the end of the file.

**Code structure inside each file**

| Piece | What it is |
|---|---|
| `S.<name>(state)` | Member screens. Each returns `{ body, fixed, pb }` |
| `T.<name>` | Trainer screens (Gym Companion, and Gym Jodi's trainer app) |
| `D.<name>` / `O.<name>` | Desktop pages (owner console / admin) |
| `C` | Components |
| `A` | Prototype actions |
| `BRAND` | Gym branding |
| `FRAMES` | Canvas frames: `[id, label, ref, state, hint, scrollTo]` |

- Put demo notes in frame hints, never in the screens.
- Before naming a new CSS class, grep for it: `.wt`, `.wk` and `.live` already exist in the base CSS and once clashed.

**Checking screens**
- Use headless Chrome, run outside the sandbox, with `--screenshot` or `--dump-dom`. The Claude-in-Chrome extension couldn't reach localhost here.
- Canvas URLs take `#f=<frame>&t=dark|light`.
- Images in `Inspiration/` are `.webp`. Convert them with `sips` before viewing.

---

## 8. Figma

Figma file `Ymy4LJVsha2qGaSKvsyq3D` was built on 26 Nov 2026.

| Page | Contents |
|---|---|
| Cover | Cover frame |
| Read me | Notes for developers, including the open plan-weight question |
| Foundations | Colour, type, spacing, radius and effects |
| Icons | 71 icon components |
| Components · Mobile | 48 components |
| Components · Desktop | 17 components |
| Gym Jodi · Member app | 39 screens; Dark row on top, Light row below |
| Platform Admin · Pilot | 8 screens, 1280 wide, Light mode |
| Exploration · Gym Companion | Locked capture |
| Exploration · Admin after pilot | Locked capture |

**Tokens and styles**
- Variable collections: Primitives, Color (Dark and Light modes), Spacing, Radius, Size. 153 variables, each with its CSS name as web code syntax.
- Styles: 25 Inter text styles and 6 effect styles.
- Light screens are clones with the Color collection's mode set to Light.

**Plugin API gotchas**
- `resize()` resets sizing modes, so set the sizing modes after resizing.
- Lay out variants manually (layout mode NONE).
- An instance swap renames the nested layer, so find icons by position.
- `setFileThumbnailNodeAsync` isn't supported.
- Calling `findAll` on a TEXT node throws.
