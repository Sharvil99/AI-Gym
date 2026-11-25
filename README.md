# Gym Companion — App Mockups

High-fidelity, interactive HTML mockups for **Gym Companion**, a B2B platform for independent gyms. AI drafts a workout plan from the gym's equipment list, a trainer reviews it and sets every weight, and the member follows it on the gym floor with a clear path to a human trainer. Owners see whether that attention actually happened.

The mockup covers the three surfaces in the Gym Companion PRD v1.0 (the **member app**, the **trainer app** and the **owner console**) Every frame is labelled with its PRD screen ID (MEM-01 … OWN-05).

The **platform admin**, where our own team onboards new gyms, is in two separate files: `App/Platform Admin Pilot.html` (what we build now, OPS-01 … OPS-04) and `App/Platform Admin.html` (the full version for after the pilot, OPS-L1 … L5). Neither is in the PRD yet.

> Sample data: member Arjun Reddy, Coach Ravi Kumar, Iron Temple Gym (Banjara Hills, Hyderabad). Names, records and numbers are illustrative.

---

## View it

No build step and no dependencies. Open the file in Chrome:

```
App/Gym Companion.html
```

The page is a design canvas:

- **00 · Prototype**: a working phone in the centre. Use **Jump to** on the left to open any member or trainer screen. State carries over, so you can call a trainer as the member, switch to the trainer and accept it, then switch back and see the status change.
- **01–43**: static frames of every screen, grouped by surface. Long screens scroll inside the phone.
- **Dark / Light** toggle in the top-right switches every screen.

Phones scale to your window height; the owner console frames scale to its width.

## Screens

| # | Section | Screens (PRD ID) |
|---|---------|------------------|
| 01–08 | Member · join & onboarding | Invite & verify, consent (MEM-01), invite expired, weight (optional), goal (MEM-02), experience & schedule, limits & symptoms (MEM-03), plan being built (MEM-05) |
| 09–16 | Member · before the workout | Plan in review (MEM-05), home & compact header (MEM-06), gym check-in (MEM-07), readiness check & hold (MEM-04), weekly plan (MEM-08), workout preview (MEM-09) |
| 17–27 | Member · in the gym | Active workout & offline (MEM-10), log a set (MEM-11), setup & technique, swap (MEM-12), get help, request sent / on the way (MEM-13), pain reported, exercise on hold, workout complete (MEM-14) |
| 28–32 | Member · AI, trainer & progress | AI Coach & daily-limit fallback (MEM-15), trainer chat (MEM-16), progress (MEM-17), 4-week check-in (MEM-18) |
| 33–38 | Trainer app | Today & queue (TRN-01), help request & resolve (TRN-04), plan review (TRN-03), member record & log a check-in (TRN-02) |
| 39–43 | Owner console (web) | Attention dashboard (OWN-01), members & follow-ups (OWN-05), orientation tracker (OWN-04), equipment inventory (OWN-03), gym & staff (OWN-02) |

## PRD rules the screens follow

- **Trainer sets the weights.** Body weight is optional and never sets loads. AI drafts arrive with no weights, and the trainer can't approve until every weight is filled in.
- **Help is honest.** A request shows *Sent* until a trainer taps accept, then *Accepted → On the way → Resolved*, each with a time. The member can say whether they got the help.
- **Pain holds only the affected exercise.** Logging that exercise is blocked and a trainer is called automatically. The rest of the workout stays open, and only a trainer can clear the hold.
- **Only the gym's equipment.** Plans, swaps and plate loading use only the gym's equipment list. Our team adds the full list in one go during setup, with no trainer verification step and no half-done drafts. The owner can mark a machine out of order, and plans skip it. Swaps wait for trainer approval. There is no "machine free now" claim without an occupancy signal.
- **Facts from logs.** Actual weight and reps are logged next to the plan. Summaries use logged sets only, with no calories or recovery percentages.
- **AI is bounded.** Standard answers come from approved cues and the plan; free text is the only AI path. At the daily limit, quick answers, logging and trainer help keep working.
- **Attention counts humans.** Owner coverage metrics count logged trainer check-ins, not automated messages or AI chats. Retention stays hidden until membership dates exist.

## Gym Jodi (beginner member app)

`App/Gym Jodi.html` is a separate, simpler version of the member app for beginners: 39 screens and an interactive prototype. It doesn't include the trainer app or the owner console.

- **3-step onboarding:** Body → Goal & schedule → Health check.
  - **Body** is one screen: an "Upload body scan" row (DEXA or InBody, PDF or photo), then Height & weight, then Body composition (optional: body fat, lean mass, fat mass, visceral fat). A report fills every tile; without one, the member types height and weight. Every value stays editable.
  - **Goal & schedule** is one screen: goal, training so far, days per week, session length and diet (Veg / Eggetarian / Non-veg / Vegan).
  - **Health check** keeps the severe-symptom hold.
- **Body scans instead of progress photos.** Photos are gone for privacy: nobody, our team included, should hold members' photos. The scan report file is kept for the member and their trainer. Engineering: encrypt it at rest, serve it only to those two, and build no admin or support view of it. Progress shows the latest scan and the change since the first scan of the same type (DEXA and InBody read differently, so they aren't compared). Members can upload a scan any time, and the 4-week check-in asks for one (optional). A scan's weight counts as that day's weigh-in.
- **No QR check-in.** The phone's location is checked once, when the member taps Start workout, against the gym's location from the admin, a Google Maps link (100 m radius). Inside: straight to the body check. Outside or location off: "Are you at Iron Temple?" Yes counts the visit and logs the mismatch as a location issue; No means the session isn't a visit and trainer help is hidden. Opening the app at the gym offers today's workout. No background tracking.
- **No logging.** Jod.ai's plan sets sets, reps and weight (weights can differ per set), and the trainer approves the plan. The exercise screen shows the current set's reps and weight in large type and lists every set; members tap a set when it's done (with an explicit Undo).
- **Couldn't complete, set by set.** "Couldn't complete" sits next to "Set N done" and opens a number scroller: the selected number sits large on a lens and its neighbours fade; drag or tap (0 = not done). The exercise carries on.
  - **Beginner rule:** missed by 1–2 reps keeps the weight; missed by 3 or more drops the remaining sets about 10% (shown as "35 kg · was 40"). Undo restores the plan.
  - **Feedback:** "How did it feel?" (Too easy / Just right / Hard, optional) appears only after a fully completed exercise. If any set was short, the reps say it and the button goes straight to the next exercise.
  - **Colour:** reps are orange when short ("32/36") and green when complete ("36/36"). Weights and feelings stay neutral.
- **Pain and stop states are calm.** Red (#E5534B dark, #CF222E light) is only an accent: the alert icon, the selected option's border and check. Hold and medical-guidance boxes are neutral cards; nothing is a filled red box.
- **Instant swaps.** The trainer approves each exercise's alternatives, with their own weights, as part of the plan, so a swap doesn't wait for anyone. Pick one and it switches; "Back to …" restores the original. Swaps work until the first set is done or the cardio timer starts, then the options are greyed out.
- **Trainer help in the action row.** How to · Swap · Trainer sit together on the exercise card. Trainer is the accent item with a ripple, and during a request it shows the status (Sent / Accepted / On the way). There's no floating button.
- **Timer only on cardio.** Treadmill, bike and similar have a countdown with pause and done. There's no rest timer and no running workout clock; total time only appears in the summary.
- **Feedback feeds the plan.** Jod.ai uses ratings and short reps when it builds the next 4-week plan; the trainer sees them when approving it.
- **Jod.ai, the AI coach:** it builds the plan on day one and restructures it every 4 weeks from progress and feedback; the trainer approves each version. In between, it answers questions in its own tab (with sources and a daily limit), and anything about pain or weights goes to the trainer.
- **Summary and progress** show time, exercises done, cardio minutes and how each exercise felt, plus the plan's weights over time. There's no volume or "best lifts", since members don't log weights.
- **Log weight** sits in the Body section header on Progress. The sheet is prefilled with the last weigh-in, with −/+ 0.1 kg or typing. It's one entry a day (logging again replaces today's), and the number, change since Aug and chart update straight away.

## Platform admin

Our dev, IT and ops team's console for onboarding gyms, in two files:

- **`App/Platform Admin Pilot.html`, built now:**
  - **Gyms:** the gym list with filters and search.
  - **Add a gym:** a 3-step wizard with Back / Next. Step 1, gym details: name, phone, email, full address (two lines, area, city, state, PIN) and the gym's Google Maps link. Coordinates are shown with "Open in Maps"; the member app uses them for its start check. Step 2, contacts: owner and point of contact (with a "Same as owner" option), each with a mobile and an optional alternate mobile, plus notes. Step 3, equipment (optional): the full list in one go, or **Do later**. The go-live date is set later on the gym's page.
  - **Gym setup:** 3 steps, all done by our team: gym details and logo, equipment, trainers. The gym opens to members on its go-live date once setup is done.
  - **Equipment:** a standalone page from Gym setup, using the same editor as wizard step 3. Search suggests equipment as you type, Paste a list matches each line, and photos are optional.
  - **Locked page:** an example of how later features appear.
- **`App/Platform Admin.html`, after the pilot:** gym pipeline, a detailed onboarding wizard (legal and tax details, plans, agreements), and provisioning. Kept as a reference.

Features that come after the pilot (leads, plans and billing, legal and tax details, agreement tracking, multiple branches, usage, support access, ops team) appear in the pilot file **locked** with an "After pilot" label. It's an internal tool, so showing them is fine, and unlocking one later is a state change rather than a redesign. Pricing stays out until PRD decision D-01 is signed off.

It uses the neutral Gym Companion brand and never shows member health data.

### Developer handoff

Open `App/Platform Admin Pilot.html` in a browser. It's one self-contained file with no build step.

1. **Working prototype** (top): click through the real flow: gym list, the Add a gym wizard with validation, Gym setup, equipment, trainers. **Fill sample data** and **Reset** sit above it.
2. **Developer rules**: every component state (default, hover, focus, filled, error, disabled; checked; selected), behaviour, validation messages and tokens with exact values.
3. **Reference screens**: static frames OPS-01 to OPS-05.

The equipment catalog behind the search is supplied by engineering: name, type, default weights and search aliases per item. The prototype uses a small sample.

## Design system

All colours are CSS custom properties, so a theme is one class swap (`.theme-dark` / `.theme-light` on `<body>`).

| Token | Dark | Light |
|-------|------|-------|
| Background | `#121212` | `#F5F5F7` |
| Card | `#1E1E1E` / `#242424` | `#FFFFFF` |
| Accent | `#D7F45B` lime | `#FF6B35` orange |
| Status | green `#3DDC84` · orange `#FF9F43` · red `#FF5A5F` | same |

Type is Inter. Cards use a 24px radius, icon buttons are 44px circles, pills are fully rounded, icons are inline Lucide-style SVG at a 1.75 stroke, and spacing follows an 8pt grid. Exercise visuals are SVG body figures with the target muscles highlighted. There are no external images.

## Per-gym branding

Every gym gets its own branded app. The gym name, city, logo and accent colours live in one object at the top of the script:

```js
const BRAND = {
  name: 'Iron Temple Gym',
  short: 'Iron Temple',
  city: 'Hyderabad',
  accent: { dark: '#D7F45B', darkInk: '#121212', light: '#FF6B35', lightInk: '#FFFFFF' },
  logo: (s) => `<svg …>…</svg>`
};
```

Change these values and every gym-facing screen updates, including the trainer app and owner console.

## Code structure

Everything is in one file: inline CSS, then inline JS.

| Part | What it holds |
|------|---------------|
| `BRAND` | Gym name, logo, accent colours |
| `ME`, `COACH`, `EX`, `SWAPS`, `TRAINERS`, `EQUIP`, … | Sample data, consistent across all three surfaces |
| `ICONS` / `icon()` | Inline SVG icon set |
| `bodyFig()` | Front and back body figure with muscle highlighting and crops |
| `C` | Shared components: phone frame, tab bars, set row, sheet, selection card, timeline, plate diagram, … |
| `S` | Member screens. Each is a function of state returning `{ body, fixed, pb }` |
| `T` | Trainer app screens, same contract |
| `D` | Owner console pages. Each returns a full desktop frame |
| `FRAMES` | What appears on the canvas: `[id, label, PRD id, state, hint, scrollTo]` |
| `A` | Prototype actions (`checkinQr`, `saveLog`, `callCoach`, `trnAccept`, `trnApprove`, …) |

### Adding a screen

1. Write `S.myScreen = (s) => ({ body: '…', fixed: '…' })` (or `T.` for the trainer app). `body` scrolls, `fixed` holds floating layers like CTAs, the tab bar and sheets.
2. Route to it in `build()` if it should be reachable in the prototype.
3. Add a line to `FRAMES`:
   ```js
   ['44', 'My new screen', 'MEM-xx', ph({ route:'myScreen' })]
   ```

## Repository layout

```
App/
  Gym Companion.html        # member app, trainer app, owner console (self-contained)
  Gym Jodi.html             # beginner member app: no logging, cardio-only timer, optional feedback (self-contained)
  Platform Admin Pilot.html # our team's console, pilot version we build now (self-contained)
  Platform Admin.html       # our team's console, full version for after the pilot (self-contained)
README.md
ROADMAP.md                  # prioritised list of future features
Roadmap Presentation.html   # the roadmap as a slide deck
```

## What's next

See [ROADMAP.md](ROADMAP.md) for future features. Note that the PRD's pilot scope leaves out several roadmap items (nutrition, gamification, payments, WhatsApp), so those aren't in this mockup.
