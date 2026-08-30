# Life Dashboard

A personal dashboard for tracking university, job applications, gym training, tasks, calendar, email and notes — as a single self-contained HTML file, with no framework, no build step, and no backend.

**[Live demo →](https://yahyaaaaay.github.io/life-dashboard-portfolio/)**

![Overview tab](screenshots/overview.png)

This repo is a sanitized demo version of a dashboard I built for my own daily use. The data here is fictional; my real copy runs privately with my own tasks, job leads, and workout log.

## What it does

The dashboard is organized as tabs, each a focused screen rather than one long scrolling page:

- **Overview** — a home screen with quick stats and a summary tile per section
- **Tasks** — a simple to-do list with categories and due dates
- **Calendar** — manually-entered dates and events, sorted upcoming-first
- **Jobs** — a lightweight application tracker (company, role, status, notes) for a job search
- **University** — program info plus a card showing how to embed any external tool via iframe
- **Gym** — the most built-out section: an exercise library (160+ movements, searchable and filterable by muscle group), a workout template builder, a set-by-set logger that shows your last performance on each exercise for progressive overload, rest timers between sets, a cardio log, and a progress/PR view
- **Emails** — a read-only snapshot view (in my real copy, connected to Gmail)
- **Files** — a categorized list of relevant documents
- **Notes** — free-form scratch space

Everything is interactive. Check off a task, log a workout, add a job lead — it all works and persists.

## How it works

**Single file, no build step.** `index.html` is the entire app: HTML, CSS and JavaScript in one file. Open it in a browser and it runs — nothing to install, nothing to compile.

**Vanilla JS, no framework.** The UI is a small hand-rolled render loop: application state lives in one JavaScript object, and every interaction re-renders the relevant part of the page from that state (`innerHTML` swaps, not a virtual DOM). Clicks and form submissions are handled through a single pair of event listeners using event delegation (`data-action` attributes), rather than binding a listener to every button.

**Two kinds of state.** Persisted state (tasks, calendar, jobs, gym data, notes, etc.) is a plain JSON object. Ephemeral UI state — which tab is active, which gym sub-view you're on, in-progress form values — is kept separately and never saved, so reloading the page always returns to a clean Overview.

**Persistence, two ways.** My private copy runs as a [Claude Artifact](https://claude.ai) and saves through Claude's `artifact` capability, so it syncs across my devices without me hosting a database anywhere. This public demo can't do that (there's no Claude session backing a GitHub Pages visitor), so it detects that at load time and falls back to your browser's `localStorage` instead — your changes persist across reloads in your own browser, and nowhere else. A "Reset demo data" button clears that and restores the sample data.

**A few small engineering details worth mentioning:**
- All user-entered text is HTML-escaped before being inserted into the page, to avoid XSS from anything typed into a form field.
- Re-rendering while typing (e.g. the exercise search box) preserves cursor position and focus, so the input doesn't feel like it's fighting you.
- The color scheme respects the system's light/dark preference and also supports an explicit manual toggle.
- The layout is responsive down to phone-sized viewports.

## Why build it this way

I wanted something I'd actually open every day, tailored exactly to what I track, without maintaining a backend, paying for hosting, or fighting a framework's opinions about how a page should be structured. A single HTML file that a browser can run directly turned out to be enough for a genuinely useful multi-section app — a nice reminder that plain JavaScript, well organized, still goes a long way.

## Running it locally

There is nothing to install. Clone the repo and open `index.html` directly in a browser, or serve it with any static file server:

```bash
git clone <this-repo-url>
cd life-dashboard-portfolio
python3 -m http.server 8000
# then open http://localhost:8000
```

## About me

I'm Yahya — starting a Computer Science degree (with a Business Administration minor) this October, focused on AI. This dashboard is one of the small tools I've built for myself along the way. Feel free to reach out if you're hiring for AI-related roles in Munich or remote.

## License

MIT — see [LICENSE](LICENSE).
