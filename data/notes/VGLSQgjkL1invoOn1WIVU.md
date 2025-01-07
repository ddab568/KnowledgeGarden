
## Project: Operation Re-write (Purposely obscure)

### Problem:

Existing site is slow and difficult to improve given it's built in wordpress. Gives limited options for improvement from a developer perspective without adding more bloat and plugins. Owned by non-for-profit therefore budget is an important consideration.

### Solution:

Re-write using headless CMS and following JAMSTACK princples.

### Existing stack

- Frontend: PHP
- Backend: PHP
- CMS: Wordpress
- DB: SQL

### Proposed re-architected stack:

- Frontend: React framework
- Backend - possibly NodeJS with GraphQL
- CMS: Headless
- DB: ?? not sure if I need one

### Rendering Style

Ref [[web.frontend.rendering-strategies]]

Options: SSR, SSG, SPA, ISR

Content is mostly static - new blog posts written relatively infrequently. There is an ecommerce section with a small number of products. No comments or anything else that is dynamic at the moment.

SSG could be a good option here but a framework that supports SSR as well could be useful for any future concerns. Maybe best of both worlds and use ISR? No need to rebuild every time we change a post or add a product.

### Framework Options

- Remix - looks good but pretty new
- Next - established, but maybe bloated for my use case? Needs a server to run for ISR and SSR
- Gatsby - only does SSG (?)

### Headless CMS Options

- Strapi - free/open source
- Contentful - recommended but paid after certain point

### DB?

Do I need?

- PSQL

## Build steps

1. Set up CMS
2. Set up FE
3. interface the two
