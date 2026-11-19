# AI Gym — Member App Mockup

A high-fidelity, interactive HTML mockup of the **member app** for a B2B gym platform. Each independent gym gives its members a branded app. AI drafts a personalised workout plan, a trainer at the gym reviews and approves it, and the member follows it on the gym floor. Members can call a trainer to their station at any time.

This first mockup covers **workout plans and the in-gym workout experience**.

> Sample data: member Arjun Reddy (28), Coach Ravi Kumar, Iron Temple Gym, Hyderabad.

---

## View it

No build step and no dependencies. Open the file in Chrome:

```
App/AI Gym App.html
```

The page is a design canvas:

- **00 · Prototype**: a working phone in the centre. Tabs, buttons, bottom sheets, set check-offs and timers all respond to clicks. Use **Jump to** on the left to open any screen, or **Reset** to start over.
- **01–11**: static frames of every screen, laid out in rows. Long screens scroll inside the phone.
- **Dark / Light** toggle in the top-right switches every screen.

Phones scale automatically to fit your window height.

## Screens

| # | Screen | Highlights |
|---|--------|-----------|
| 01–03 | Onboarding | Weight ruler (drag it) with BMI card, goal picker, animated "plan being built" checklist ending in coach review |
| 04 / 04b | Workout home | Sticky header and week strip that shrink on scroll, program card with coach approval, today's workout, streak, muscle recovery rings |
| 05 | Plan | 8-week overview, week chips, day-by-day breakdown, coach's note |
| 06 | Workout detail | KCAL / time / volume, target muscle rings, AI load adjustment, warm-up toggle, exercise list |
| 07 | Active workout logger | Set rows with animated check-offs, rest timer (−15s / +15s / pause), AI weight suggestion, Timer / AI tip / Swap, always-visible **Coach** button |
| 08 / 08b | Help sheet | Call a coach to my station, message, form check, swap a busy machine, report pain → "Ravi is on his way" state |
| 09 | Workout complete | Summary stats, muscles worked, "How did it feel?" feedback, PRs |
| 10 | Coach tab | Trainer card, chat with voice note, shared workout, AI weekly recap reviewed by the coach |
| 11 | Profile | Goal progress, stats, weight trend chart, measurements, progress photos, strength sparklines, settings |

A **Workout in progress** mini-bar appears above the tab bar on every tab while a workout is running.

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

Change these values and every screen updates.

## Code structure

Everything is in one file: inline CSS, then inline JS.

| Part | What it holds |
|------|---------------|
| `BRAND` | Gym name, logo, accent colours |
| `ME`, `COACH`, `EX`, `WEEK`, … | Sample data, consistent across screens |
| `ICONS` / `icon()` | Inline SVG icon set |
| `bodyFig()` | Front and back body figure with muscle highlighting and crops |
| `C` | Reusable components: phone frame, status bar, nav, tab bar, mini-bar, rings, set row, bottom sheet, avatar, sparkline |
| `S` | Screens. Each is a function of app state returning `{ body, fixed, pb }` |
| `FRAMES` | What appears on the canvas, in order |
| `A` | Prototype actions (`start`, `check`, `help`, `callCoach`, …) |

### Adding a screen

1. Write a function `S.myScreen = (s) => ({ body: '…', fixed: '…' })`. `body` scrolls, `fixed` holds floating layers like CTAs, the tab bar and sheets.
2. Route to it in `build()` if it should be reachable in the prototype.
3. Add a line to `FRAMES` to show it on the canvas:
   ```js
   ['12', 'My new screen', () => ({ ...freshState(), route: 'myScreen' })]
   ```

## Repository layout

```
App/
  AI Gym App.html   # the mockup (self-contained)
README.md
ROADMAP.md                  # prioritised list of future features
Roadmap Presentation.html   # the roadmap as a slide deck
```

## What's next

See [ROADMAP.md](ROADMAP.md) for future features, ranked by priority and the value each adds for members and gyms. To present it, open `Roadmap Presentation.html` in Chrome and use the arrow keys (F for fullscreen).
