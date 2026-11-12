# KT Terminal

**Personal project.** A self-hosted, multi-asset "Bloomberg-style" trading terminal: command-driven panel shell, live streaming feeds and a paper-trading account. No API keys required, so it runs and demos immediately.

## Stack

FastAPI, SQLAlchemy, SQLite, pandas/numpy · React 18, TypeScript, Vite, Zustand, TradingView Lightweight Charts · Playwright + Vitest (210 tests) · Docker Compose, CI.

## What I built

- Command-driven panel shell with TradingView Lightweight Charts.
- Live crypto plus delayed equities and macro feeds, with no API keys needed to run.
- Paper-trading account, watchlist, depth, positions, blotter, news, macro and options scanner.
- **210 tests** — Playwright for end-to-end, Vitest for unit — with Docker Compose and CI.

## Engineering notes

The interesting problems are the ones a chat UI never forces you to solve: partial data, out-of-order updates, reconnects and a fixed frame budget. Each panel subscribes to a slice of the stream rather than the whole feed, so a slow render in the options scanner cannot stall the blotter.

I built this on my own initiative to keep the real-time and testing habits sharp between client projects. It is the piece of work I point to when someone asks how I actually test a streaming UI.

## Code access

The repository is private. I can share a recorded walkthrough covering the live feed, the paper trade and the test run.
