# Pomodoro Timer

A single-file desktop Pomodoro timer with atmospheric minimal design. Open the file in a browser — no install, no build, no dependencies.

![Screenshot](https://img.shields.io/badge/status-ready-brightgreen)

## Features

- **Drift-free timer** — uses `Date.now()` instead of counting intervals, stays accurate even when the tab is backgrounded
- **Web Audio chimes** — C major triad on work completion, descending notes on break completion, no audio files needed
- **Atmospheric dark UI** — SVG noise texture, breathing glow ring animation, `prefers-reduced-motion` support
- **Auto-switch** — work → break → work with a 2-second grace period
- **Session tracking** — persisted to `localStorage`, displayed as dot indicators
- **Browser notifications** — alerts when a session ends and the tab is hidden
- **Customizable** — collapsible settings panel for work/break durations
- **Keyboard shortcuts** — Space (start/pause), R (reset)

## How to use

```
# Open in browser (Windows)
start pomodoro.html
```

No server, no `npm install`, no build step. Works offline from the filesystem.

## Default durations

| Mode | Duration |
|------|----------|
| Work | 25 minutes |
| Break | 5 minutes |

Change in Settings (gear icon). Work: 1–60 min, Break: 1–30 min.

## Tech stack

Zero dependencies. HTML5 + CSS3 + vanilla JavaScript.
