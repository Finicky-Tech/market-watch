---
layout: default
title: Market Watch · Finicky Technologies Ltd
---

# Market Watch

A crowdsourced food price tracking platform for Nigeria, built with the
long-term goal of complementing — and eventually feeding into — the
National Bureau of Statistics' (NBS) Consumer Price Index methodology.

This file is the entry point for the Market Watch project: where the code
lives, where the documentation lives, and what state each part is in.

---

## Repositories

| Repository | Stack | Role |
| --- | --- | --- |
| `market-watch-api` | NestJS, TypeORM, PostgreSQL, PGMQ | Backend API. Clean Architecture + DDD + CQRS-lite; NestJS treated as external infrastructure, not the core. |
| `market-watch-ui` | Angular, Signal Forms, Tailwind CSS | Frontend. Vertical-slice / domain-driven folder structure (`data/`, `features/`, `ui/`, `utils/`). |

Both repositories share the same architectural values: no ceremony without
a proven runtime need, and explicit, honest repetition over clever
abstractions that obscure intent.

---

## Documentation

| Document | Purpose |
| --- | --- |
| [Market Watch: Closing Nigeria's Food Price Gap](./sales/white-paper_09-08-2026/market-watch-white-paper.md) | The problem/solution white paper — the primary external-facing document, written for a non-technical audience up to and including NBS, legislators, and policy analysts. |

Documentation for the API and frontend systems currently lives alongside
each repository rather than in this shared docs set.

---

## Status Snapshot

### API System (`market-watch-api`)

- IAM module (`identity`, `authentication`, `authorization`) complete.
- Multi-channel notification system complete.

### Platform UI (`market-watch-ui`)

- Auth feature in progress.

### Product

- No live public dataset yet. The white paper leans on architecture
  soundness and external precedent (the JRC/FPCA crowdsourcing pilot)
  rather than results, and says so plainly.
- Domain modelling (UML class diagram, informal-unit normalization for
  Nigerian market units) is in early conceptual stages.

---

## Company

Market Watch is built and operated by **Finicky Technologies Ltd**
(CAC registration in progress), a Nigerian web development startup.

---

*This index is a living document. Update it as repositories, documents,
or status change — it should always reflect where the project actually
stands, not where it stood at time of writing.*
