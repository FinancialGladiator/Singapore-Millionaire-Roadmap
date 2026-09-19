# The Singapore Millionaire Roadmap

**In Singapore, a fast-food worker can retire a millionaire.**

That's the claim this app puts to the test. Plug in your own age, salary and household situation, and it runs a month-by-month projection — CPF, taxes, SRS, housing, a diversified STI + SRS portfolio — all the way to age 65, to show what compounding, CPF, and a handful of deliberate habits actually add up to over a working life.

**Live demo:** https://financialgladiator.github.io/Singapore-Millionaire-Roadmap/

---

## What it is

A no-backend web app, installable straight to your phone's home screen. No sign-up, no server — every projection runs entirely in your own browser; nothing you type is ever sent anywhere.

It's built around six tabs:

1. **The Claim** — the hook, and a live preview: enter your own age, salary and household type right on the cover screen and watch the projected net worth update as you type. Once you've used the full calculator on Tab 2, this preview switches to mirror your complete scenario — condo, car, growth mode, custom allocations and all — instead of its own bare-bones estimate.
2. **Your Number** — the full calculator. Housing (BTO/resale/condo), career assumptions, a "work till age" slider for anyone planning to stop earning before 65 (CPF LIFE still can't legally start early, so the gap between stopping work and 65 is bridged from your own STI pot, with CPF and SRS left untouched to keep compounding), CPF LIFE choices, allocation across Necessities/Wants/SRS/STI, a net worth chart running to retirement — marked with milestones (first S$100k, millionaire, multi-millionaire) at the age each one actually lands, and toggleable between future dollars and today's dollars — live warnings whenever a condo upgrade or car purchase would be beyond your budget, and a set of "what if" one-tap scenarios (start 5 years earlier, skip the car, save half of every raise, and so on).
3. **How It Works** — the playbook, step by step, and the maths behind every figure the calculator produces, for anyone who wants to check the working.
4. **What Breaks It** — ten common traps that derail the plan (lifestyle inflation, the car, no CPF nomination, marrying someone unaligned on money, and more), each with its own fix.
5. **Go Further** — seven principles for the portfolio itself (including a one-tap "add a rebalance reminder to your calendar" button, since the discipline only works if you actually do it), an interactive diversification simulator, a seven-country comparison of how long it takes to save a home deposit on the same wage, and a searchable glossary of every term used across the app.
6. **Legal & Contact** — why this was built, the full disclaimer, and how to get in touch.

Also built in:

- A 10-question financial literacy quiz, with your own score compared against Singapore's self-reported national average.
- Shareable results: a downloadable image card (in two formats — a detailed scorecard, or a vertical Story-shaped version for Instagram/TikTok), plus native sharing straight to WhatsApp, Messenger, Mail and anything else your phone's share sheet offers.
- A shareable scenario link that encodes your own inputs into the URL, so you can send someone your exact numbers to try for themselves.
- Installable as a PWA — add it to your home screen on Android/Chrome via the install prompt (or iOS Safari's Share → Add to Home Screen), and it opens full-screen like a native app, with the last-loaded version cached for offline use.

---

## Methodology

Built from a month-by-month simulation, age 20 to 65 (or from whatever age you start at, if not 20). Housing prices, EHG grant tiers and CPF parameters are drawn from HDB/CPF sources (2025–26 rates); the STI is modelled at a 6% total return with dividends reinvested; headline figures are discounted to today's dollars at 2.5%/yr to strip out the effect of decades of assumed inflation. Every one of these assumptions is laid out in full on Tabs 2 and 3, with the exact formula behind each figure.

Choosing to stop working before 65 doesn't stop the simulation at that age — CPF LIFE is fixed by law to start at 65 (or later, if deferred) no matter how early you actually retire, and CPF/SRS keep compounding with zero new contributions in the meantime, exactly as they would in reality. Necessities and Wants freeze at whatever they were the year you stop working, inflated forward, and are drawn from your STI pot to bridge the gap — so the model shows the real cost of an early retirement, not just a truncated projection.

Any committed cost the household genuinely can't cover — a downpayment that outstrips both CPF and savings, a purchase that would leave income negative — is carried forward as debt that keeps compounding against the household, rather than silently disappearing from the numbers. Where a choice is being priced (the true cost of a car, a condo upgrade, five years of lifestyle inflation), the comparison always displaces the full committed amount, independent of how much room that month's budget happened to have.

This is an illustration of what the numbers say is *possible* under a specific, stated set of assumptions — not a forecast, and not personalised financial advice. Markets don't move in a straight line, rules and thresholds change, and real circumstances vary. Verify specifics against the official HDB and CPF sites, and speak to a licensed adviser for decisions that matter.

---

## Tech stack

The app itself — markup, styling, and logic — lives in one HTML file, with a small service worker and web app manifest alongside it for installability. No build step, no package manager, no framework, no dependencies.

- Vanilla JavaScript for the calculation engine and all interactivity
- Plain CSS (no preprocessor)
- Inline SVG for the charts; the Canvas API for the shareable image cards
- The Web Share API for native sharing, where the browser supports it
- A minimal service worker (network-first, falling back to cache) for offline access and installability, registered only when served over HTTPS — it's a no-op if you just open the `.html` file locally

---

## Running it locally

Download `index.html` and open it directly in any modern browser — that's it. There's nothing to install and nothing to build. (The install-to-home-screen and offline features won't be available this way — those need a real HTTPS origin, see below.)

To host it yourself with full installability (e.g. on GitHub Pages, as above): push these five files to a repo, keeping `index.html` at the root and the rest alongside it, and enable Pages for that repo:

- `index.html`
- `manifest.json`
- `sw.js`
- `icon-192.png`, `icon-512.png`, `icon-512-maskable.png`, `icon-180.png`, `icon-32.png`

No other configuration is needed. If you'd rather keep it to a single file, that's fine too — just don't add the manifest link and icon references from `index.html`'s `<head>`; the app itself doesn't depend on any of them.

---

## Disclaimer

Illustration only, not financial advice. CPF is simplified (wage ceiling, allocation, Medisave and CPF LIFE approximated); tax uses current resident brackets; the salary curve, return and raise split are all stated assumptions, not guarantees. Your real figures will differ from what this app shows you — verify anything that matters against IRAS, CPF and HDB directly, and speak to a licensed adviser before making decisions based on any of this.

---

## Credits

Built by Financial Gladiator, iterating conversationally with Claude.

Feedback, bug reports, and ideas for what young Singaporeans actually need from a tool like this are always welcome — see the Legal & Contact tab in the app for how to get in touch.
