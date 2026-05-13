# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install       # install dependencies (required before first run)
npm run dev       # start dev server at http://localhost:5173
npm run build     # production build to dist/
npm run preview   # preview production build locally
npm run lint      # run ESLint
```

There is no test suite configured.

## Architecture

This is a single-file React app — all logic and UI live in [src/App.jsx](src/App.jsx). There are no sub-components, routing, or external state management libraries.

**State shape in `App`:**
- `transactions` — array of `{ id, description, amount, type, category, date }`. `amount` is stored as a string (not a number), which causes incorrect arithmetic in `totalIncome`, `totalExpenses`, and `balance` (known bug).
- Form state: `description`, `amount`, `type`, `category` — controlled inputs for adding a new transaction.
- Filter state: `filterType`, `filterCategory` — drive the visible subset of transactions.

**Known intentional issues (course material):**
- `amount` stored as string → `reduce` concatenates instead of summing.
- "Freelance Work" is categorized as `type: "expense"` despite being income.
- UI styling is minimal/unstyled beyond [src/App.css](src/App.css).
