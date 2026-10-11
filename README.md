# BudgetFlow — Broke But Functional

A responsive personal-finance challenge app: make ₹10,000 last 30 days.

## Features
- Live balance, daily allowance, month-end forecast and financial-health score
- Expense logging, category breakdown, daily spending chart and CSV export
- Upcoming commitments that affect your allowance and forecast
- Savings goals with progress tracking
- Decision Lab for purchases, unexpected bills and extra income
- Browser-local persistence and resettable demo data

## Run locally
Open `index.html` in a modern browser, or run `python -m http.server 4173` and visit `http://localhost:4173`.

## Deploy
This is a static single-page app with no build step. Deploy the repository root on Vercel, GitHub Pages, or another static host.

## Data note
This demo stores data in the current browser's `localStorage`. It does not connect to banks, process payments, or sync across devices.
