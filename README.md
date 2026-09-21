# Northwind — E-commerce Website

A small, static e-commerce website built with plain HTML, Tailwind CSS (CDN) and
a handful of front-end libraries. It contains a marketing landing page, two
authentication pages, and an analytics dashboard — all sharing one dark theme.

This is a **front-end demo**: there is no backend, no database and no real
payments. All data on the dashboard is mock data defined inline in the page.

## Pages

| Page | File | What it is |
|------|------|------------|
| Home / landing | [`index.html`](index.html) | Company introduction: hero, services, metrics, mission, testimonial and call-to-action sections |
| Sign in | [`login.html`](login.html) | Email + password form with client-side validation and social sign-in buttons |
| Sign up | [`register.html`](register.html) | Full registration form (name, email, password + confirm, optional phone/address, terms consent) |
| Dashboard | [`charts.html`](charts.html) | Analytics report with three tabs: Overview, Top 10 sellers and Regional revenue |

The pages link to one another: the landing page routes to sign-in / sign-up and
to the dashboard demo, and the auth pages link back to each other.

## Features

**Landing page**
- Animated hero with a drifting "aurora" background and a mouse-driven 3D tilt
- Animated gradient headline, count-up statistics and scroll progress bar
- Infinite marquee of customer logos
- Reveal-on-scroll animations, hover lift and glow on cards
- Responsive layout for mobile, tablet and desktop

**Auth pages**
- `novalidate` forms with JavaScript validation and inline error messages
- Rules: valid email, password ≥ 8 characters, matching confirmation,
  10-digit phone (optional fields may be left blank)
- Password show/hide toggle, "remember me", demo toast notifications

**Dashboard**
- KPI tiles (revenue, orders, average order value, net profit)
- Chart.js line, bar and doughnut charts for revenue, categories, channels,
  traffic sources, employee ranking and regional revenue
- Tables with growth deltas and status badges
- Date-range filter (7D / 30D / 90D / 12M) and a channel filter
- Every chart has a "view as table" fallback for accessibility

## Tech stack

Everything loads from a CDN at runtime, so no build step or install is needed:

- [Tailwind CSS](https://tailwindcss.com/) — utility styling, configured inline in each page
- [Chart.js 4](https://www.chartjs.org/) — charts on the dashboard
- [Lucide](https://lucide.dev/) — icon set
- [Animate.css](https://animate.style/) — entrance animations on the landing page
- [Google Fonts](https://fonts.google.com/) — Poppins (headings) and Inter (body)
- [Unsplash](https://unsplash.com/) — photography on the landing page

> An internet connection is required to load the CDNs and the Unsplash images.

## Design system

Colors, fonts and conventions are documented in [`CLAUDE.md`](CLAUDE.md). In short:

- Dark theme with a `#090A14` page background and orange `#DF6B33` brand accent
- Poppins for headings, Inter for body text
- Consistent focus states, `prefers-reduced-motion` support and accessible labels

## Running locally

No installation required — open a page directly in a browser:

```
start index.html        # Windows
open index.html         # macOS
```

Or serve the folder over HTTP for a cleaner origin:

```
python -m http.server 8000
# then visit http://localhost:8000
```

## Project structure

```
.
├── index.html      # landing page
├── login.html      # sign-in
├── register.html   # sign-up
├── charts.html     # analytics dashboard
├── CLAUDE.md       # design rules and conventions
├── README.md       # this file
└── .gitignore
```

## Notes and limitations

- All figures, names and campaigns are illustrative mock data.
- Form submissions are simulated with a toast and a timeout — wire them to a real
  endpoint (e.g. `fetch()`) before using this in production.
- Images are hot-linked from Unsplash; review their license and consider hosting
  your own assets before a public launch.

## License

Demo project, provided as-is for learning and reference. Third-party assets
(libraries, fonts and photographs) remain under their respective licenses.
