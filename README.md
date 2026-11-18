# investment-service-backend

Holdings, trades and valuations.

Part of [Finance Master](https://github.com/financemaster-proj/platform) — a
personal finance system built as four backend services behind an API gateway.

## What this service owns

Instruments, holdings, trades and valuation snapshots. Cost basis and realised/unrealised P&L.

## What it does not own

Expenses or reports. It is the only service that talks to an external market data provider, and does so behind a circuit breaker.

## Interface

| | |
|---|---|
| Port | `8083` |
| Database | `fm_investment` |
| Emits | `TradeExecuted`, `PortfolioValued` |
| Consumes | `UserDeleted` |

## Running locally

Infrastructure lives in the [`platform`](https://github.com/financemaster-proj/platform)
repo. Clone it as a sibling of this one, then:

```bash
cd ../platform && docker compose -f infra/docker-compose.yml up -d
cd - && cp .env.example .env && ./gradlew bootRun
```

## Conventions

This service follows the project-wide rules in
[`platform/docs`](https://github.com/financemaster-proj/platform/tree/main/docs) —
in particular **no synchronous calls to another service**
([ADR-0004](https://github.com/financemaster-proj/platform/blob/main/docs/adr/0004-no-synchronous-service-calls.md)),
package by feature, Flyway for every schema change, and money as `BigDecimal`
with an explicit currency.
