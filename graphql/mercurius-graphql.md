# Mercurius GraphQL

Mercurius is a GraphQL adapter for Fastify. It exposes a GraphQL endpoint that handles queries, mutations, and subscriptions over HTTP and WebSocket.

## Endpoint

By default Mercurius mounts the GraphQL endpoint at `/graphql` on the Fastify server instance. This is configurable at registration time via the `path` option.

## Key Capabilities

- **Just-In-Time Compilation** — Uses `graphql-jit` to compile GraphQL queries to optimized JavaScript functions, significantly reducing execution overhead on repeated queries.
- **Query Caching** — Parsed and validated queries are cached so that identical query strings skip parse/validate on subsequent requests.
- **Automatic Dataloader Integration** — Built-in loader support prevents N+1 problems without requiring manual batching setup.
- **Subscriptions** — Real-time subscriptions delivered over WebSocket (`graphql-ws` protocol).
- **Federation** — Full Apollo Federation v1/v2 support via `@mercuriusjs/federation` and `@mercuriusjs/gateway` packages.
- **Batched Queries** — Supports array-style batched GraphQL requests in a single HTTP call.
- **Persisted Queries** — Configurable persisted query support to reduce request payload size and improve security.
- **GraphQL Playground** — Built-in GraphiQL/Playground UI available in development mode.

## Installation

```bash
npm install mercurius
```

## Basic Usage

```js
import Fastify from 'fastify'
import mercurius from 'mercurius'

const app = Fastify()

const schema = `
  type Query {
    hello(name: String): String!
  }
`

const resolvers = {
  Query: {
    hello: async (_, { name }) => `Hello, ${name ?? 'World'}!`
  }
}

app.register(mercurius, {
  schema,
  resolvers,
  graphiql: true
})

app.listen({ port: 3000 })
```

## Resources

- GitHub: https://github.com/mercurius-js/mercurius
- npm: https://www.npmjs.com/package/mercurius
- Documentation: https://mercurius.dev/
