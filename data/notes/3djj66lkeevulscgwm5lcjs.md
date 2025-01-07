
General guide for achieving good SEO for website:

Three Pillars of optimization according to NextJS:
1. **Technical** - optimization/performance of the website
2. **Creation** - ensuring optimal content creation to target specific keywords
3. **Popularity** - Using backlinks (third party sites linked back to your own) so that search engines know you are a trusted source. Having an online presence. 


**Web crawlers** are a type of bot that mimic end users and navigate links found on websites in order to perform indexing for search engines. They identify themselves through custom [user-agents](https://developers.google.com/search/docs/advanced/crawling/overview-google-crawlers). 


#### Notes on improving SEO
- Build a sitemap
- Use SSR or SSGs - see [[web.frontend.rendering-strategies]]. SPAs usually don't use url paths and loading time is not ideal for a crawler.
- Use metadata such as `<title>` and `<meta name="description" content="A good description here">` on every page
  -  robot tags are directives search engines will respect e.g. `<meta name="robots" content="noindex,nofollow">` . These meta tags can be produced on demand as opposed to robots.txt
  - canonical tags to prevent the detection of duplicate content
- Ensure good performance e.g. response time
- Use alt for images
- Use meaningful status codes
   - 200 in general
   - 301 for redirects to indicate permanently moved. Next JS Uses 308 redirects instead to preserve request methods used. 302 and 301s change the request method of the redirect to a GET
- Use semantic HTML - the correct and most relevant tags
- Use a good URL structure e.g. semantic urls /learn/nextjs-app-course vs /courses/1

In November 2020, Google added three new metrics to their page experience signals called Core Web Vitals:

- Largest Contentful Paint (LCP) - The amount of time it takes to render the largest content element within the viewable area of the screen e.g. featured image
- First Input Delay (FID) - the time between the first users input and when the page responds (responsiveness)
- Cumulative Layout Shift (CLS) - visual stability of a page - checking for "janky-ness" where the screen shifts

### Largest Contentful Paint (LCP)

Common causes of poor LCP:

- **Slow server response times **- The first thing to look at is Time to First Byte (TFFB) and see if that can be improved.

- **Render blocking JS and CSS** - style sheets and javascript imports will block the HTML parser. Defer any non-critical JavaScript & CSS. CSS and JS files can be minified.

- Slow resource load times - optimize and compress images

- Client side rendering - If you're building a site that is mostly rendered on the client, you should be wary of the effect it can have on LCP if a large JS bundle is used.

### References

1. https://nextjs.org/learn/seo/crawling-and-indexing/status-codes
2. https://nextjs.org/learn/seo/rendering-and-ranking/rendering-strategies