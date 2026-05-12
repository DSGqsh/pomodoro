# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

A single-file desktop Pomodoro timer (`pomodoro.html`). Zero dependencies, no build step — open the file in a browser to run.

## How to run

```
# Open in default browser (Windows)
start pomodoro.html
```

No server, no `npm install`, no build. The app works offline from the filesystem.

## Architecture

All code lives in `pomodoro.html`. The embedded JS is organized into five modules operating on a single `state` object:

| Module | Key functions | Purpose |
|--------|--------------|---------|
| **Timer** | `startTimer`, `pauseTimer`, `resetTimer`, `tick`, `completeSession` | Countdown logic. Uses `Date.now()` for drift-free timing rather than decrementing on each `setInterval` tick. |
| **UI** | `renderRing`, `renderTimeDisplay`, `renderControls`, `renderAll`, `updateDocTitle` | Reads state and updates DOM nodes. Each function targets a specific element — no global re-render. |
| **Sound** | `playChime`, `playWorkComplete`, `playBreakComplete` | Web Audio API sine-wave chimes. AudioContext is lazily created on first user interaction. |
| **Storage** | `loadPersistedState`, `savePersistedState` | Persists settings + session count to `localStorage`. Timer runtime state is never stored. |
| **Settings** | `toggleSettings`, `saveSettings` | Collapsible panel for work/break duration with validation (1-60 min work, 1-30 min break). |

### State object

The single `state` object drives everything. Fields prefixed with `_` are internal timing state and are not persisted:

```
status: 'idle' | 'running' | 'paused' | 'finished'
mode: 'work' | 'break'
workDuration, breakDuration — in seconds
timeRemaining — in seconds
sessionsCompleted — persisted across page reloads
_startTimestamp, _pausedRemaining, _intervalId, _autoStartTimeoutId — internal only
```

### Timer accuracy

`tick()` runs every 200ms via `setInterval` but calculates elapsed time from `Date.now()` rather than counting ticks. This means the timer stays accurate even when the browser tab is backgrounded and `setInterval` is throttled.

### CSS

Dark theme using custom properties on `:root`. Mode-switching (work/break) works by updating `--accent` and the ring/button colors via JS — CSS transitions handle the smooth color crossfade.