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

React + Vite app with no routing or external state management. `transactions` state lives in `App` and is passed down as props. There are no shared constants files — `categories` is duplicated in `TransactionForm` and `TransactionList`.

**Component breakdown:**
- [src/App.jsx](src/App.jsx) — owns `transactions` state and `handleAdd`; renders the four child components.
- [src/Summary.jsx](src/Summary.jsx) — receives `transactions`, computes `totalIncome`, `totalExpenses`, and `balance` internally.
- [src/TransactionForm.jsx](src/TransactionForm.jsx) — owns its own form state (`description`, `amount`, `type`, `category`); calls `onAdd(transaction)` prop on submit.
- [src/TransactionList.jsx](src/TransactionList.jsx) — owns filter state (`filterType`, `filterCategory`); receives `transactions` and renders the filtered table.

**Transaction shape:** `{ id, description, amount, type, category, date }` — `amount` is a number, `type` is `"income"` or `"expense"`.

**Known issue (course material):**
- "Freelance Work" is categorized as `type: "expense"` despite being income.
