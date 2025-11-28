# Angular 21 Highlights

**Angular 21** was released on Nov. 20, 2025 and it feels truly exciting. As someone who has worked with Angular since the AngularJS days - through **Ivy**, **Standalone Components**, and recently **Signals** - this release feels like a real paradigm change.   
Angular officially becomes **zoneless** and the mental model shifts toward **Signals** - a recent reactive paradigm within the Angular framework. This shift also brings Angular closer to the wider JavaScript ecosystem.

Here are the updates that stand out for me:

**1. ARIA Accessibility Library (Developer Preview)**   
   The team built a modern library for common UI patterns with **accessibility as the #1 priority**. It uses modern directives, is signal-based, and builds on their deep experience - you just need to add styles and business logic.   
   Accessibility isn't just “nice to have” - it is a security and compliance requirement by **WCAG**, **ADA**, and **EAA (the European Accessibility Act)**. This shows the Angular team takes accessibility seriously - helping us learn best practices directly from them.

**2. Vitest Support (Stable)**   
   Angular officially announces **Vitest as the default test runner**! Finally, we say goodbye to Jasmine/Karma performance issues. Vitest is fast, supports in-browser testing, and handles ESM natively (unlike Jest).
   For me, this is a major mindset shift toward modern tooling.

**3. Signal Forms (Experimental)**   
   With Signal Forms, the Form model is defined by a signal that automatically syncs with bound fields. This offers an intuitive developer experience with full type-safety and built-in, centralized schema validation.   
   This continues the transition toward a signal-first architecture, simplifying mental models and aligning with the framework's future.

**4. Angular MCP Is Stable**   
   This is exciting - official, stable MCP support brings **AI-assisted workflows into everyday Angular development**. It bridges the "knowledge cutoff." Your AI agent can now access up-to-date docs, learn modern patterns and best practices, and understand new features like Signal Forms instantly.   
   A serious step toward modern AI-assisted programming.

**5. Zoneless by Default (Stable)**   
   Angular is officially **zoneless**. With signals driving state management, `zone.js` (which patches browser APIs) is no longer needed.
   No zone.js dependency → **fewer errors**, **better performance**, **easier debugging**, and **ecosystem compatibility**. I experimented with this in `v20.2` and it looks seamless.

It’s fascinating to watch Angular evolve and be part of this community. The team listens, delivers, and keeps pushing the ecosystem forward.

>**Note:** Please check these features status by the time you read the knowledge - this information is up to date as of Nov. 20 release date of Angular21.

## Documentation and References
For diving deeper into these concepts, here are some great resources by the Angular Team and Community experts:

**1. Announcing Angular v21 by the Angular Team**
 - [What's new in Angular v21 - Angular 21 Highlights in Creative YouTube Video Format](https://www.youtube.com/watch?v=DDAHORVzQ5g&t=6s)
 - [The official "Announcing Angular v21" blog post by the Angular team on Medium](https://blog.angular.dev/announcing-angular-v21-57946c34f14b)

**2. Angular ARIA**
   - [Angular ARIA - Official Docs by Angular Team](https://angular.dev/guide/aria/overview)

**3. Vitest**
   - [Migrating from Karma to Vitest - Official Docs by Angular Team](https://angular.dev/guide/testing/migrating-to-vitest)
   - [Vitest Overview for Angular](https://youtu.be/tKulEWNnI1s?si=MFFRfWw_nLxojuzz) by Rainer Hahnekamp

**4. Signal Forms**
- [Angular Signal Forms - Official Docs by Angular Team](https://angular.dev/guide/forms/signals/overview)
- [All About Angular’s New Signal Forms](https://www.angulararchitects.io/en/blog/all-about-angulars-new-signal-forms/) by Manfred Steyer
- [Angular Signal Forms – Part 1](https://blog.ninja-squad.com/2025/11/04/angular-signal-forms-part-1) by Cédric Exbrayat

**5. Angular MCP and AI Assisted Engineering**
 - [Angular AI – Official Resource Hub for AI-powered Apps by Angular Team](https://angular.dev/ai)
 - [Angular CLI MCP Server setup - Official Docs by Angular Team](https://angular.dev/ai/mcp)
 - [Angular CLI MCP Server: The Complete Guide to All Available Tools](https://www.codigotipado.com/p/angular-cli-202-meets-ai-the-complete) by Amos Isaila

**6. Angular without ZoneJS (Zoneless)**
- [Angular without ZoneJS (Zoneless) - Official Docs by Angular Team](https://angular.dev/guide/zoneless)
