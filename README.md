# 🪂 Parachute

Interactive, browser-based remakes of the analog self-assessment exercises popularized by *What Color Is Your Parachute?* by Richard N. Bolles. Each is a single, self-contained page — no sign-up, no server, works offline, and saves your progress in your browser.

**Live:** https://anewt225.github.io/parachute/

---

## Tools

### 🗳️ [Prioritizing Grid](https://anewt225.github.io/parachute/prioritizing-grid/)

Rank any list by the classic **pairwise-comparison** method: instead of trying to order everything at once, you judge one pair at a time — *this, or that?* — and the tool tallies the wins into a ranking.

- **Enter any number of items** and see the total number of comparisons up front, so the cognitive workload is never a surprise.
- **One-pair-at-a-time flow** with full keyboard control, plus the original **triangular grid** view with live tallies.
- **Real tiebreakers** — items that finish tied are re-compared (or, for a three-way-plus tie, ordered directly) rather than resolved silently.
- **Express mode** — an optional faster path that skips any comparison your earlier answers already imply (if A > B and B > C, it takes A > C as given), cutting a 10-item ranking from 45 comparisons to roughly 20.
- **Clean export** — copy or download the result as a plain numbered list.

---

## Why pairwise comparison?

Ranking many things at once exceeds working memory (people reliably hold only ~3–4 items in mind at a time), which is why long ranked lists feel arbitrary. Comparing two things at a time keeps every decision inside that limit and forces explicit trade-offs, avoiding the "everything is high-priority" problem of rating scales.

The trade-off is volume: comparing every pair is *O(n²)* — 45 comparisons for 10 items. The **express mode** addresses that by exploiting transitivity (a binary-insertion ranking), which only ever asks what your previous answers haven't already settled, at *O(n log n)*. The default full mode is kept because it also *surfaces* inconsistent preferences (A > B > C > A cycles) that the express mode assumes away.

## Design & implementation notes

- **Zero dependencies.** Plain HTML, CSS, and vanilla JavaScript in one file per tool. Nothing to build, nothing to install.
- **Offline-first.** No network calls; state persists via `localStorage`.
- **Accessible & responsive.** Keyboard navigation, visible focus states, `prefers-reduced-motion` support, and light/dark theming via `prefers-color-scheme`.
- **A neutral slate palette with a single burnt-orange accent** reserved for the active/selected state, so what's interactive always reads as interactive.

## Repository layout

```
parachute/
├── index.html            landing page
├── prioritizing-grid/
│   └── index.html         the tool (self-contained)
├── README.md
└── LICENSE
```

Adding a tool = a new folder with its own `index.html`, plus a card on the landing page.

## Running locally

Everything is static, so just open a file in a browser — or serve the folder:

```bash
python -m http.server 8000
# then visit http://localhost:8000
```

## License

[MIT](LICENSE) © Alex Newton.

Original exercises inspired by *What Color Is Your Parachute?* by Richard N. Bolles. This project is an independent, original reimplementation and is not affiliated with or endorsed by the book or its publisher.
