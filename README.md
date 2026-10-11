# BudgetFlow — Broke But Functional

BudgetFlow is a responsive personal-finance challenge app that helps a user make ₹10,000 last 30 days.

## Product goal

The app turns a fixed 30-day budget into an interactive planning workspace. A user can record spending, reserve money for commitments, create savings goals, test hypothetical decisions, and review a forecast before changing the plan.

## Core modules

| Module | What works |
|---|---|
| Overview | Live balance, spend pace, daily allowance, forecast, health score, chart and category breakdown |
| Transactions | Add, validate, list, remove and export expenses as CSV |
| Commitments | Add future commitments, validate dates/amounts, remove them and include them in forecasts |
| Savings goals | Create goals, add savings, track progress and remaining target |
| Decision Lab | Simulate purchases, unexpected expenses and extra income; optionally commit decisions to the plan; remove decision records |
| Money insights | Average spend, projected month-end, health/risk message and category analysis |
| Challenge tracker | Persistent 30-day start date and day progress |
| Persistence | Browser-local localStorage with defensive state normalisation |
| Responsive UI | Desktop/tablet/mobile layouts with a compact mobile navigation |
| Accessibility | Skip link, keyboard-visible focus, native dialog controls, labels/ARIA semantics, reduced-motion support |
| Data export | CSV export with spreadsheet-formula injection protection |

## Financial model

- Starting budget: ₹10,000.
- Challenge length: 30 days.
- Balance = starting budget + committed extra income − recorded expenses.
- Commitments are reserved in the allowance and month-end forecast.
- Daily spending pace is calculated from recorded expenses divided by the current challenge day.
- Decision Lab uses the current spending pace for the projected remainder instead of double-counting the simulated purchase.
- Savings goals are planning targets and do not silently remove cash from the balance until an expense is actually recorded.

## Data and security

This is a client-side demo. It does not connect to banks, process payments, or transmit financial records to a server.

- User-entered names are HTML-escaped before dynamic rendering.
- Persisted categories and decision types are normalised against an allow-list.
- Numeric amounts are bounded and validated before writes.
- Malformed localStorage data is handled defensively.
- CSV values beginning with =, +, -, or @ are neutralised to reduce spreadsheet formula-injection risk.
- A restrictive Content Security Policy is included for the static document.
- No third-party analytics or tracking code is used by the application.

## Accessibility

BudgetFlow includes:

- Skip-to-content navigation.
- Native buttons and forms rather than click-only div controls.
- Visible focus indicators.
- Accessible labels for form controls.
- aria-live status toast.
- Native dialog for confirmation and data-entry actions.
- tablist/tab semantics for the main module tabs.
- aria-current and aria-selected state updates.
- Reduced-motion support.
- Responsive keyboard-friendly controls.

## Quality and QA

Before deployment, the inline application script is syntax-checked with JavaScript Function compilation. The implementation also guards against malformed persisted state and validates user-controlled numeric/text inputs.

Recommended smoke-test matrix:

1. Open Overview and switch through every module.
2. Add an expense from the header and Transactions module.
3. Remove an expense and confirm balance/forecast update.
4. Add and remove a commitment.
5. Create a savings goal and add savings.
6. Run Decision Lab simulations for purchase, unexpected expense and income.
7. Commit a decision and verify the corresponding transaction/income effect.
8. Remove a committed decision record.
9. Change chart range.
10. Export CSV and open it in a spreadsheet.
11. Refresh the page and verify data persistence.
12. Reset demo data and verify the 30-day challenge restarts.
13. Test at mobile width and with keyboard-only navigation.
14. Test with browser reduced-motion enabled.

## Run locally

No build step is required.

~~~bash
python -m http.server 4173
~~~

Open http://localhost:4173.

Opening index.html directly also works in modern browsers, although using a local HTTP server is preferred for consistent browser behavior.

## Deployment

The repository is a static site. Deploy the repository root with a static hosting provider.

Current production project: **budgetflow-vert-six**

## Repository structure

~~~text
budgetflow/
├── index.html     # application UI, styles and client-side application logic
└── README.md      # product, data model, security, accessibility and QA documentation
~~~

The single-file structure is intentional for zero-build portability: the project can be copied to a static host and run without Node dependencies.

## Data limitations

Data lives only in the current browser's localStorage:

- It is not synced across devices.
- Clearing site data removes the saved state.
- It is not a banking or accounting system.
- It should not be used as a source of truth for regulated financial records.

## License

This project is provided as an educational portfolio/demo application.
