# Mercurius

High-performance GraphQL server for Fastify with Just-In-Time compilation, query cache, federation support, subscription via WebSocket, and GraphQL Playground integration.

- **Website:** https://mercurius.dev/
- **Documentation:** https://mercurius.dev/
- **GitHub:** https://github.com/mercurius-js
- **npm:** https://www.npmjs.com/package/mercurius
- **License:** MIT

## Overview

Mercurius is a GraphQL adapter for Fastify. It wraps the standard `graphql-js` runtime with significant performance enhancements and a rich plugin ecosystem, making it the recommended way to add GraphQL to any Fastify application.

### Key Features

- **JIT Compilation** — Compiles GraphQL queries to native JavaScript via `graphql-jit`, reducing execution overhead on hot paths.
- **Query Cache** — Parse and validation results are cached so identical query strings bypass repeated processing.
- **N+1 Prevention** — Automatic dataloader integration batches and deduplicates resolver calls.
- **Subscriptions** — Real-time GraphQL subscriptions delivered over WebSocket.
- **Federation** — Full Apollo Federation support for building distributed GraphQL architectures.
- **Batched Requests** — Accepts arrays of GraphQL operations in a single HTTP request.
- **Persisted Queries** — Allowlist-based query registration to reduce payload size and improve security.
- **Playground** — GraphiQL UI available in development mode.

## Catalog Contents

| Path | Description |
|---|---|
| `apis.yml` | Machine-readable catalog entry (apis.io format) |
| `graphql/mercurius-graphql.md` | GraphQL endpoint and usage reference |
| `plans/mercurius-plans.md` | Licensing and plan overview |
| `rate-limits/mercurius-rate-limits.md` | Rate limiting guidance |
| `finops/mercurius-finops.md` | Cost and FinOps considerations |

## Maintainer

Kin Lane — kin@apievangelist.com
