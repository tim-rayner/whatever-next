# Lib Module (tRPC client utilities)

## Client-side usage (Client Components)

Import `api` from `~/lib/trpc` for tRPC hooks:

```ts
import { api } from '~/lib/trpc'

const { data } = api.hello.greet.useQuery({ name: 'world' })
const mutation = api.posts.create.useMutation()
```

`TrpcProvider` must wrap any subtree that uses client-side tRPC hooks — it is already added in `src/app/layout.tsx`.

## Server-side usage (Server Components / Route Handlers)

Import from `~/lib/trpcServer` for direct server-side calls (no HTTP round-trip):

```ts
import { trpc } from '~/lib/trpcServer'

const data = await trpc.hello.greet({ name: 'world' })
```

Use this in `page.tsx` Server Components and `generateMetadata` functions.
