# Frontend Rendering Models
Choosing the correct rendering model (**CSR**, **SSR**, **SSG**, **Hydration**) based on your project needs ensures good performance, accessibility, and faster loading times.

The following frontend rendering models are available today:

- [Client-Side Rendering (CSR)](#client-side-rendering-csr)
- [Server-Side Rendering (SSR)](#server-side-rendering-ssr)
- [Static Site Generation (SSG)](#static-site-generation-ssg)
- [Hydration](#hydration)

## Client-Side Rendering (CSR)
**Client-Side Rendering (CSR)** means the browser renders HTML from JavaScript after downloading it.
- Client-side rendering has the simplest development model, as you can write code that assumes it **always runs in a web browser**. This lets you use a wide range of **client-side libraries** that also assume they run in a browser.
- It generally has **worse performance** than other rendering modes, as it must download, parse, and execute your page's JavaScript before the user can see any rendered content. If your page fetches more data from the server during rendering, users also have to wait for those additional requests before they can view the complete content.
- If your page is indexed by search crawlers, client-side rendering may **negatively affect SEO**, as search crawlers have limits on how much JavaScript they execute when indexing a page.
- With client-side rendering, the server doesn't need to do any work beyond serving static JavaScript assets. This can be an advantage if **keeping server costs low** is a concern.
- Applications that support installable, offline experiences with [service workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) can rely on client-side rendering without needing to communicate with a server.

## Server-Side Rendering (SSR)
**Server-Side Rendering (SSR)** means that the server generates the HTML for the page, which is then sent to the browser to render.
- Server-side rendering offers **faster page loads** than client-side rendering. Instead of waiting for JavaScript to download and run, the server directly renders an HTML document upon receiving a request from the browser. The user experiences only the **latency needed for the server to fetch data and render the page**. This mode also eliminates the need for additional network requests from the browser, as your code can fetch data during rendering on the server.
- Server-side rendering generally provides **excellent SEO**, as search crawlers receive a fully rendered HTML document.
- It requires you to author code that **does not strictly depend on browser APIs**, and it **limits your selection of JavaScript libraries** that assume they run in a browser.
- With server-side rendering, your server runs the frontend technology to produce an HTML response for every request, which may **increase server hosting costs**.

## Static Site Generation (SSG)
**Static Site Generation (Pre-rendering)** means that pages are pre-built at build time and served as static files.
- Pre-rendering offers **faster page loads than both client-side and server-side rendering**. Because it **creates HTML documents at build time**, the server can directly respond to requests with the static HTML document without any additional work.
- Pre-rendering requires that all **information needed to render a page is available at build time**. This means prerendered pages cannot include user-specific data. It is primarily useful for **pages that are the same for all users**.
- Because prerendering occurs at build time, it may **add significant time to your production builds**. Using `getPrerenderParams` to produce many HTML documents may increase deployment size and **slow down deployments**.
- It generally provides **excellent SEO**, as search crawlers receive a fully rendered HTML document.
- Like SSR, it requires code that **does not depend on browser-only APIs**, and limits certain JavaScript libraries.
- Pre-rendering incurs **very little overhead per server request**, as your server only returns static HTML. These static files can be **easily cached** by CDNs, browsers, and other caching layers, making it especially useful for **high-traffic applications**. Fully static sites can be deployed via CDN or static file servers, **eliminating the need for a server runtime** and improving scalability.

## Hydration

**Hydration** is a core concept in modern web application **performance** and **interactivity optimization**, especially in frameworks like **React**, **Angular**, **Svelte**, and **Astro**.
- It refers to the process of **attaching JavaScript behaviors to a server-rendered or statically-generated HTML page so that it becomes interactive**.  
  Without hydration, interactivity (clicks, inputs) won’t work even if content is visible.
- Hydration is the process of **receiving a static HTML page** (from **SSR** or **SSG**) and **re-attaching** the client-side JavaScript logic (event listeners, state handling, etc.) to that `HTML`.  
  This enables interactivity without requiring a full re-render from scratch on the client.
- There are different types of hydration supported: **Full Hydration**, **Incremental Hydration**, **Partial Hydration**

**When Does Hydration Happen?**  
Hydration typically follows:
- **Server-Side Rendering (SSR)**: HTML is rendered per request on the server.
- **Static Site Generation (SSG)**: HTML is pre-rendered at build time.  
  In both cases, when the browser loads the HTML page, it also downloads the JavaScript bundle to hydrate the page.

**Pros and Cons of Hydration**

| ✅ Pros                                 | ❌ Cons                                                  |
| -------------------------------------- |-----------------------------------------------------------|
| Faster initial content load (good LCP) | Large JS bundle required (especially with full hydration) |
| Improves SEO (especially with SSR)     | Can delay interactivity (TTI)                             |
| Better perceived performance           | Full hydration can be wasteful for static content         |

### Full Hydration
**Full Hydration** is the process when the **entire page** is rendered on the server, then fully hydrated on the client.
- This is common in SSR frameworks like **Next.js** (default), **Angular Universal**, **Nuxt.js**.
- **Example:** React (Next.js): When a page is SSR rendered and the full React app takes over client-side, performing reconciliation to make it interactive.

**Pitfalls with Full Hydration**
- The entire app rehydrates even if only some parts need interactivity.
- More JavaScript to parse, load, and execute.

### Incremental Hydration
In the case of **Incremental Hydration**, entire `HTML` is still server-rendered or statically built, **but hydration is deferred** per component or block.
- The whole app could eventually be hydrated, but hydration is delayed and done **incrementally** based on user interactions, visibility, or defined triggers.
- **Example1:** Angular supports this via `@defer` blocks with **hydrate triggers**.
    ```
    @defer (on viewport) {
      <expensive-component></expensive-component>
    }
    ```
- **Example2:** React (with Next.js App Router) can achieve incremental hydration through `Suspense` combined with **server-side streaming**, allowing portions of the page to become interactive progressively as they are streamed from the server and their client components hydrate.
    ```
    <Suspense fallback={<Skeleton />}>
      <HeavyComponent /> {/* This component or its children might contain client-side interactivity */}
    </Suspense>
    ```

**Benefits of Incremental Hydration**
- Reduces JS execution cost.
- Faster Time to Interactive.
- Lazy loads only what’s needed.

### Partial Hydration (aka Islands Architecture)
**Partial hydration** is an optimization technique in server-side rendering (SSR) or static site generation (SSG) where the **entire HTML page is rendered on the server**, but only **specific interactive components** - typically small, isolated parts of the UI **are hydrated with JavaScript on the client**.
- Instead of hydrating the whole page, the framework sends JavaScript only for the interactive parts, significantly reducing the client-side JavaScript bundle size and improving load and interaction performance.
- This approach enables **high performance** and **fast initial page loads**, especially useful for content-heavy pages with limited interactivity (e.g., marketing pages, blogs, documentation).
- A common implementation of partial hydration is the **Islands Architecture**, where the page is composed of mostly static HTML (rendered on the server), but small "islands" of interactivity are hydrated on the client.
    - Each island is a self-contained interactive component.
    - Islands do not depend on global hydration.
    - This pattern is used by frameworks like **Astro**, **Eleventy**, and even **Next.js with React Server Components**, when only a few components are marked as "use client".

**Benefits of Islands / Partial Hydration**
- **Reduced** JavaScript **bundle size**
- **Faster** Time To Interactive (**TTI**)
- **SEO-friendly** (due to full server-rendered HTML)
- Fine-grained control over interactivity

**Example: Partial Hydration in React Server Components (RSC) with Next.js**  
React Server Components allow you to define components that run only on the server and selectively mark others to run on the client, achieving partial hydration.  
This reduces the amount of JavaScript sent to the browser and improves performance.  
In this example:
- The `Page` component is rendered on the server — it has no interactivity.
- The `ClientButton` is explicitly marked as a client-side component using `'use client'`.
- During hydration, only `ClientButton` is hydrated, and not the rest of the page.

This is a clear example of partial hydration — only the interactive part (`ClientButton`) is hydrated, while the rest remains static.

```tsx
// app/page.tsx (Server Component by default)
import ClientButton from './ClientButton';

export default function Page() {
    return (
        <main>
            <h1>This is rendered on the server</h1>
            <ClientButton />
        </main>
    );
}
```

```tsx
// app/ClientButton.tsx
'use client'; // This line makes the component run on the client

import { useState } from 'react';

export default function ClientButton() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>Clicked {count} times</button>;
}
```

### Hydration: Comparison Table
Hydration is crucial for building performant web apps that balance server-side rendering with client-side interactivity.   
Understanding the differences between full, incremental, and partial hydration helps in selecting the right rendering strategy for your application.   
Modern frameworks often allow you to mix and match strategies to optimize for **speed**, **interactivity**, and **developer ergonomics**.

| Feature             | **Full Hydration**         | **Incremental Hydration**      | **Partial Hydration (Islands)** |
| ------------------- |----------------------------|--------------------------------|---------------------------------|
| Rendered on Server  | ✅                          | ✅                              | ✅                            |
| JS Hydration Type   | Entire Page                | Per block/component            | Only interactive components     |
| Hydration Trigger   | Page Load                  | Interaction / Viewport         | Client-directive (manual)       |
| JS Bundle Size      | High                       | Moderate                       | Low                             |
| Interactivity Speed | Slower                     | Faster                         | Fastest                         |
| Examples            | Angular Universal, Next.js | Angular @defer, React Suspense | Astro, React Server Components  |


## Rendering Models: Comparison and When to Choose Each

| Rendering Type                    | ✅ Pros                                                                                   | ❌ Cons                                                                                      | How it works?                                                                                                         | When to Choose                                                                                                            |
|-----------------------------------|-------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| **Client-Side (CSR)**             | - Simple dev setup<br> - Full browser API support<br> - Lowest server cost                | - Slower performance<br> - Poor SEO<br> - JS must fully load to render                      | The server sends the initial minimal HTML, the client downloads the JavaScript and renders the entire UI dynamically. | **SPAs, Web applications, low-SEO needs, offline/PWA use cases**                                                           |
| **Server-Side (SSR)**             | - Fast initial load<br> - Great SEO<br> - Server-side data fetching                       | - Higher server cost<br> - No browser-only libs<br> - Angular runs on each request          | The server renders HTML, sends to the client for display                                                              | **SEO-critical sites, user-specific data on first load, content heavy websites**                                           |
| **Prerendering (SSG)**            | - Fastest page load<br> - Great SEO<br> - CDN caching<br> - Zero server load per request  | - Build-time data only<br> - Slower build time<br> - Not for dynamic or user-specific pages | The server generates static HTML, the client uses JavaScript to update                                                | **Websites that require fast initial load times and dynamic updates, static content, marketing pages, blogs, docs**        |
| **Partial/Incremental Hydration** | - Improved performance<br> - Reduced JavaScript<br> - Fine-grained control                | - More complex setup<br> - Framework-dependent<br> - Still evolving as a standard           | SSR/SSG pre-renders HTML; only selected interactive components are hydrated client-side                               | **Sites that benefit from fast static delivery but still need interactivity (e.g., dashboards, e-commerce product pages)** |
