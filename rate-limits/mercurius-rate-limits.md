# Mercurius Rate Limits

Mercurius is a self-hosted, open-source library. It does not impose rate limits of its own — all resource constraints are determined by the infrastructure on which you deploy it.

## No Built-In Rate Limiting

Out of the box, Mercurius does not enforce:

- Request-per-second or request-per-minute caps
- Query complexity limits (beyond basic validation)
- Depth limits
- Payload size caps (beyond Fastify defaults)

## Controlling Load at the Fastify Layer

Because Mercurius runs as a Fastify plugin, you can apply rate limiting using standard Fastify ecosystem tooling:

| Tool | Purpose |
|---|---|
| `@fastify/rate-limit` | Per-route or global request-rate limiting with Redis or in-memory backends |
| `@fastify/throttle` | Token-bucket throttling for bandwidth control |
| Fastify request hooks | Custom middleware to reject requests above a threshold |

## GraphQL-Level Protections

Mercurius supports several mechanisms that indirectly bound resource consumption:

- **Persisted Queries** — Only pre-registered query hashes are executed, preventing arbitrary expensive ad-hoc queries.
- **Query Depth / Complexity Rules** — Custom GraphQL validation rules can be added via the `validationRules` option to reject deeply nested or expensive queries.
- **`@mercuriusjs/validation`** — Schema-level input validation to reject malformed or out-of-range arguments early.
- **`@mercuriusjs/cache`** — Response caching reduces redundant resolver execution for repeated queries.

## Infrastructure-Level Rate Limits

When deploying Mercurius in production, rate limiting is typically handled upstream:

- **Reverse proxy / API gateway** (nginx, Caddy, AWS API Gateway, Cloudflare Workers) apply HTTP-level rate limits before traffic reaches the Fastify process.
- **Cloud provider limits** (memory, CPU, connection count) bound throughput at the platform layer.

## References

- Fastify rate-limit plugin: https://github.com/fastify/fastify-rate-limit
- Mercurius security docs: https://github.com/mercurius-js/mercurius/blob/master/docs/security.md
- Persisted queries: https://github.com/mercurius-js/mercurius/blob/master/docs/persisted-queries.md
