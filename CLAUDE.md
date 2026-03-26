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

The app is split into four components:

- **`App`** — holds the `transactions` array in state and passes data/callbacks down. No logic beyond `handleAdd`.
- **`Summary`** — receives `transactions`, computes `totalIncome`, `totalExpenses`, and `balance` internally.
- **`TransactionForm`** — owns its own form field state; calls `onAdd(transaction)` prop on submit.
- **`TransactionList`** — receives `transactions`, owns `filterType` and `filterCategory` state, derives filtered list on render.

There is no routing, context, or external data layer. The `categories` array is duplicated in `TransactionForm` and `TransactionList`.

**State shape:** Each transaction has `{ id, description, amount, type, category, date }` where `type` is `"income"` or `"expense"` and `amount` is a number.
