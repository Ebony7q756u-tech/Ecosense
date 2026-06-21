# EcoSense — Personal Carbon Intelligence

Track, understand and reduce your personal carbon footprint, with
India-specific emission factors and AI-powered insights (Claude or
Gemini — bring your own API key).

Built as a single-page app with no build step, no framework, and no
server: open `index.html` and it runs. All data stays on-device in
`localStorage`.

## Features

- **Activity logging** — Transport, Food & Diet, Home Energy, and
  Shopping, each with India-calibrated emission factors (e.g. CEA 2023
  grid intensity, Indian Railways averages).
- **Carbon Score & Planetary Health Meter** — a 0–100 daily score and a
  visual gauge of your footprint against a fair daily carbon budget.
- **AI Insights** — daily/weekly analysis, a reduction plan, a monthly
  forecast, a weekly coaching message, and a free-form AI chat, all
  powered by a Claude or Gemini key you supply and which is sent only
  to the official provider endpoints.
- **Tools** — photo/receipt scanner (AI-read electricity bills,
  receipts, fuel slips), voice logging, an "AI Debate Mode" that
  fact-checks climate claims, India-specific carbon offset links, a
  shareable carbon card, PDF/HTML report export, and city-level
  emission-factor overrides (Delhi, Mumbai, Bengaluru, Chennai, Patna,
  Hyderabad, Kolkata, Pune).
- **Goals, Challenges & Achievements** — monthly targets with progress
  rings, ten daily challenges, seven unlockable achievements, and a
  weekly leaderboard.
- **Compare & History** — your footprint vs. India/global/regional
  averages, a 7-day trend chart, and full activity history.
- **Accounts** — email/password auth (SHA-256 hashed, stored locally)
  with a guest mode, session expiry + lock screen, and a first-run
  onboarding flow that estimates a baseline footprint.

## Running it

No install, no build:

```
open index.html
```

(or serve the folder with any static file server, e.g. `npx serve .`)

AI features (Insights, Chat, Photo Scanner, Voice Logging, Debate Mode,
Weekly Coach) require a Claude or Gemini API key, entered in the
Dashboard's **AI API Keys** panel. Keys are stored only in the
browser's `localStorage` and are sent only to the official Anthropic /
Google endpoints (see the Content-Security-Policy `connect-src` in
`index.html`).

## Testing

A standalone, dependency-free Node test suite exercises the app's core
calculation engine — `CO2_FACTORS`, `calcScore`, `getGrade`,
`escapeHtml`, and all reference data tables — directly against the
real `index.html`, with no mocking of the business logic itself (only
the DOM is shimmed).

```
npm test
```

This also re-runs the app's own in-browser self-test panel
(`runSelfTests()`, exposed in the running app via **Tools → Run
Self-Tests** or the floating 🔧 button) and asserts every check in it
passes too, so the in-app diagnostics and the CI suite can never
silently drift apart.

CI runs the same suite on every push via GitHub Actions
(`.github/workflows/test.yml`).

## Architecture

`index.html` is intentionally a single file (no bundler, no
dependencies to install, easy to audit) but is internally organised
into clearly-commented sections — see the architecture overview comment
near the top of the `<script>` block:

1. **DATA** — static reference tables (countries, challenges,
   achievements, emission factors, city factors)
2. **UTILITIES** — `escapeHtml()`, `debounce()`, `safeLS*()` helpers
   used throughout to keep rendering XSS-safe and input handling
   efficient
3. **STATE (`S`)** — a single in-memory store persisted to
   `localStorage`, always accessed through the `safeLS*` wrappers so a
   blocked or corrupted storage environment never crashes the app
4. **CALCULATIONS** — `CO2_FACTORS` + `calcScore` + related pure
   functions, kept side-effect-free so they're independently testable
5. **RENDERING** — `render*()` functions that update the DOM
6. **FEATURES** — auth, AI integration, voice input, photo scan, goals,
   challenges, reports, offsets
7. **DIAGNOSTICS** — the self-test harness described above

## Security & accessibility notes

- A strict `Content-Security-Policy` and `X-Content-Type-Options:
  nosniff` are set via meta tags; only Anthropic, Google (Gemini +
  Sign-In) and Google Fonts origins are allow-listed.
- All AI/OCR/voice-parsed text is passed through `escapeHtml()` before
  being inserted via `innerHTML`, to prevent stored/DOM XSS from
  untrusted model output.
- Passwords are SHA-256 hashed before storage (this is a client-only
  demo with no backend — see the in-app note on the password-reset
  screen).
- An accessibility auto-enhancer runs on load and after every DOM
  mutation, filling in missing `aria-label`s, marking decorative icons
  `aria-hidden`, and giving the tab bar proper `role="tablist"`/`role="tab"`
  semantics, without altering any existing markup or behaviour.

## Encoding

This repo intentionally pins UTF-8 + LF line endings via
`.gitattributes` for every text file. The project previously lost all
of its emoji and em dashes when a tool round-tripped the file through
a non-UTF-8 codepage — if you edit `index.html`, make sure your editor
saves as **UTF-8 without a BOM** to avoid a repeat.
