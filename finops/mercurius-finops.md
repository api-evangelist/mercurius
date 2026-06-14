# Mercurius FinOps

Mercurius is MIT-licensed open-source software with no licensing costs. All financial considerations relate to the infrastructure you use to self-host it.

## Software Cost

| Item | Cost |
|---|---|
| Mercurius npm package | Free |
| All official plugins (@mercuriusjs/*) | Free |
| Updates and new releases | Free |

## Infrastructure Cost Drivers

Because Mercurius is self-hosted, your total cost of ownership depends on the following variables:

### Compute

- **Node.js process footprint** — Mercurius is lightweight. The JIT compilation step uses additional CPU on first query execution per process lifecycle but reduces CPU on repeat queries.
- **Instance type** — A single low-cost VPS (1–2 vCPU, 512 MB–1 GB RAM) is sufficient for moderate traffic; scale horizontally behind a load balancer for production workloads.
- **Serverless** — Mercurius can run in serverless environments (AWS Lambda, Fly.io, Render, Railway) where you pay per invocation rather than for idle capacity.

### Memory

- The query cache and JIT-compiled function cache consume heap memory proportional to the number of unique query shapes in your workload. Monitor heap usage and tune cache size limits accordingly.

### Networking

- GraphQL over HTTP is typically low-bandwidth per request.
- WebSocket subscriptions hold persistent connections; factor connection concurrency into instance sizing and load-balancer costs.

### Federation / Gateway

- Running a Mercurius gateway that fans out to multiple subgraph services multiplies compute and network costs by the number of services involved.

## Cost Optimization Strategies

| Strategy | Benefit |
|---|---|
| Enable persisted queries | Reduces payload size and eliminates query-parse CPU on repeat requests |
| Use `@mercuriusjs/cache` | Cuts redundant resolver execution and downstream DB/API calls |
| Enable JIT (default on) | Reduces per-request CPU after warm-up, lowering compute cost at scale |
| Batch queries | Fewer HTTP round-trips per client session |
| Deploy behind CDN for public queries | Cache at edge; zero origin compute for cacheable responses |

## Monitoring Tools

- **`mercurius-explain`** — Measures the cost (time) of each GraphQL query resolver; useful for identifying expensive resolvers to optimize or cache.
- **Fastify metrics plugins** (`@fastify/metrics`, `fastify-prometheus`) expose request latency and throughput for infrastructure right-sizing.

## References

- npm package: https://www.npmjs.com/package/mercurius
- mercurius-explain: https://github.com/mercurius-js/mercurius-explain
- Fastify deployment guide: https://fastify.dev/docs/latest/Guides/Serverless/
