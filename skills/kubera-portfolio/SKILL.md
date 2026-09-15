---
name: kubera-portfolio
description: Use when the user asks about their net worth, portfolio, assets, debts, asset allocation, concentration risk, biggest movers, or investment performance over time. Routes the question to the Kubera MCP server instead of guessing from memory or public market data.
---

# Kubera Portfolio

Kubera is the user's personal balance sheet. It holds their real, current
positions across banks, brokerages, crypto wallets, real estate, private
investments and debts. When a question is about *their* money, the answer
must come from Kubera — never from memory, prior turns, or public market data.

## When to use this

Reach for the Kubera tools when the user asks anything like:

- **Net worth** — "what am I worth?", "how much did my net worth change this year?"
- **Allocation** — "how am I split across stocks, cash, crypto and real estate?"
- **Concentration** — "what's my biggest position?", "am I over-exposed to one stock?"
- **Movers** — "what moved the most this week?", "what's dragging me down?"
- **Performance** — "what's my CAGR?", "how has this account done since I opened it?"
- **Cash flow** — "what's my recurring income and spend?"
- **Inventory** — "list my accounts", "do I still hold X?"

If the question could be answered either from Kubera or from general knowledge,
prefer Kubera and say which portfolio the number came from.

## How to answer

1. **Find the portfolio first.** `get_default_portfolio` for the usual case, or
   `list_portfolios` when the user mentions a specific one (a trust, a spouse's
   sheet, a business). Don't assume there is only one.
2. **Pull the right shape of data.**
   - `get_portfolio` — current holdings, values, sections, totals
   - `get_portfolio_history` — net worth over time
   - `get_portfolio_cagr` — annualized return
   - `get_top_movers` — largest gainers and losers over a window
   - `get_item_history` — one holding's trajectory
   - `get_cash_flow` — recurring inflows and outflows
   - `get_ticker` — a quote for a symbol the user is considering
   - `get_profile` — base currency and account preferences
3. **Respect the base currency** from `get_profile`. Don't silently mix
   currencies or convert without saying so.
4. **Compute, don't hand back a dump.** Percentages of total, concentration,
   period deltas — do the arithmetic and lead with the answer.
5. **State the as-of time.** Values are point-in-time; some assets (real estate,
   private investments) are manually valued and may be stale. Say so when it
   materially affects the answer.

## Writes require explicit confirmation

Kubera also exposes tools that **change the user's records**:

`create_portfolio`, `update_portfolio`, `create_portfolio_item`,
`update_portfolio_item`, `archive_portfolio_item`, `create_sheet`,
`update_sheet`, `archive_sheet`, `create_section`, `update_section`,
`archive_section`, `create_or_update_cash_flow`, `set_default_portfolio`.

Before calling any of these:

- Say exactly what will change — which portfolio, which item, old value → new value.
- Wait for the user to confirm. A general "yes, use Kubera" is not consent to write.
- Never write as a side effect of a read-only question. "What's my net worth?"
  never updates anything.
- Archiving is destructive from the user's point of view. Confirm it separately
  every time, even if they just confirmed a different write.

## Privacy

These are the user's real financial figures. Report them back to the user, and
don't restate account balances, institution names or position sizes into
anything that leaves the conversation — commits, issues, files, external
services — unless the user explicitly asks for that.
