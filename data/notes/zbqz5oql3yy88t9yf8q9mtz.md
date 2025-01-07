
## Post 14.0 notes and usage

### Routing

In version 13, Next.js introduced **App router**. Prior to this, Next used page router.

The difference from the outset means that prior to 13, users would place their routes within a `pages/` directory where each file is considered a route:

```
└── pages
    ├── about.js
    ├── index.js
    └── team.js

```

With 13 onward, app router looks for a `pages.(js|ts|tsx)` file who's route is determined by it's parent folders. Eg:

```

└── app
    ├── about
    │   └── page.js
    ├── globals.css
    ├── layout.js
    ├── login
    │   └── page.js
    ├── page.js
    └── team
        └── route.js

```

Subfolders (leaves) become nested routes.

App router is the recommended approach in modern NextJS projects. Page router is still supported.

App router is built on **React Server Components** (RSC) By default, components inside app are RSC components.

### File conventions

Nextjs has various reserved file names that provide common inbuilt routing functionality:

- `layout.js` - a shared segment between pages that preserves states, remains interactive and doesn't re-render. The top most layout is known as the **_Root layout_** and it is required component that is shared by all pages in the application. It must contain a html and a body tag.
- `template.js`
- `error.js` - handles errors in routes
- `loading.js` - creates a loading view. Beneath the hood it's tied in with Suspense in the layout file.
- `not-found.js` - view for an unknown route
- `page.js` or nested `layout.js`

### Data Fetching

#### On the server

By default, Next.js automatically caches the return values of `fetch` in a built-in **Data Cache** on the server.

If data is dynamic or requires re-validation, cached data needs to be purged. There are two ways to re-validate:

- Time based - revalidate once a certain amount of time has passed. This is useful for data that doesn't change frequently and freshness is not critical. This is good for a mostly static website.

```js
fetch("https://...", { next: { revalidate: 3600 } });
```

- On-demand revalidation - manually revalidate data based on an event. This is on par with traditional server side rendering to ensure that data is always fresh on every request.

If you want a request to opt-out of caching, you need to set a `no-store` option in the fetch call:

```js
// Opt out of caching for an individual `fetch` request
fetch(`https://...`, { cache: "no-store" });
```

Alternatively, you can use the route segment config option to opt out of caching for a specific route segment:

```js
// Opt out of caching for all data requests in the route segment
export const dynamic = "force-dynamic";
```

#### On the client

Fetching data on the client can be done via a Route Handler or a third party library such as Vercel's [SWR](https://swr.vercel.app/) or [TanStack Query](https://tanstack.com/query/latest).

Route Handlers execute on the server and therefore protect sensitive information.

Route handlers replace the API routes from 13.0 onward (although API routes can still be used).

### Data fetching recommendations

Next.js recommends that whenever possible, to fetch data on the server with server components. This is done via server actions.

Server actions are react functions that are asynchronous and are executed on the server. They can be denoted via the "use server" directive, can be inline or within a separate file.

```jsx
// Server Component
export default function Page() {
  // Server Action
  async function create() {
    'use server'

    // ...
  }

  return (
    // ...
  )
}
```
