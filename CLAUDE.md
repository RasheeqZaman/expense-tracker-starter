# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install       # Install dependencies (required first time)
npm run dev       # Start dev server at http://localhost:5173
npm run build     # Production build
npm run lint      # Run ESLint
npm run preview   # Preview production build
```

> Note: Vite v7 requires Node 20+. This repo uses Vite v5 for compatibility with Node 18.

## Architecture

This is a single-component React app. All state and logic lives in `src/App.jsx` — there are no child components, routing, or external data layer.

**Known bugs (intentional, part of the course):**
- `amount` is stored as a string in state, so `reduce` does string concatenation instead of numeric addition — totals are wrong
- Transaction #4 ("Freelance Work") is marked `type: "expense"` but categorized as `"salary"` — a data inconsistency

**State shape:** Each transaction has `{ id, description, amount, type, category, date }` where `type` is `"income"` or `"expense"` and `amount` is a string (bug).

**Filtering:** `filteredTransactions` is derived inline on each render from `filterType` and `filterCategory` state — no memoization.
