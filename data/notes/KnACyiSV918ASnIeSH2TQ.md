
## CSR (Client-Side Rendering) / SPA (Single Page Application)

> the data is fetched after every single render

Most common way of using frameworks such as React, vue, ember etc.

Client-side rendering means that a website’s JavaScript is rendered in your browser, rather than on the website’s server.

- The server renders a blank page with a script tag pointing to the apps bundle
- blank page is sent to the clients browser which makes the relevant api calls and renders the contents of the page

strengths:

- renders fast on the server

weaknesses:

- no initial render - customer/client has to render so if the app is big it could be a problem

- empty body - no content to crawl for a search engine - ** SEO is the biggest weak point **

## SSR (Server Side Rendering)

> the data is fetched before every single render

When the user makes a request to the webpage, the server prepares the html page and then sends it back.

## SSG (Static-Site Generating)

> the data is fetched once at build time

Page is also generated on the server however it is rendered at **build time.**

## ISR (Incremental Static Regeneration)

> the data is fetched once on build time and will be fetched again after a certain cooldown and served on the second visit.

Allows you to create or update static pages after you've built your site. This gives you the benefit of using static generation without needing to rebuild the entire site.

## When to use what?

- Is your content dynamic or relatively static?

- is SEO important?

Here are some examples from [this article](https://medium.com/codex/web-design-patterns-ssr-ssg-and-spa-fadad7673dfe#:~:text=SSR%20vs%20SSG,I%20use%20SSR%20then%3F%22.)

> For a documentation page or a website that doesn't need to fetch dynamic data, but SEO is important, you could use SSG.
> For a blog, SEO is important and the content is dynamic. In this case, SSR could be a good candidate.
> For a CRM (Customer Relationship Manager), SEO is not a concern and the content is dynamic therefore an SPA/CSR would be a good choice.

Many websites will use a combination. These days for anything that is not an SPA, it's often recommended to use SSG practically all of the time unless there is a good reason not to e.g. the website is massive with dynamic content that cannot be pre-rendered as it changes frequently. [Next JS recommends SSG ](https://nextjs.org/docs/basic-features/pages#pre-rendering) for many use cases. The alternative is to use ISR for a website with mostly static content but for a web page with thousands of pages in order to prevent a complete rebuild every time.

> "We recommend using Static Generation over Server-side Rendering for performance reasons. Statically generated pages can be cached by CDN with no extra configuration to boost performance. However, in some cases, Server-side Rendering might be the only option."

Some important considerations:

1. Data Integrity - how fresh do we want the data? CSR and SSR fetch on every render.

2. SEO - SSR, SSG and ISR are SEO friendly given crawlers don't have to wait for a page to load to get relevant data
3. Performance - SSG and ISR load instantly (for first contentful paint)
4. Build Time - the amount of time it takes to build and deploy the website is slower for SSG and ISR since we need to build all the pages to serve where as CSR and ISR build pages dynamically.

##### References

1. https://theodorusclarence.com/blog/nextjs-fetch-usecase
