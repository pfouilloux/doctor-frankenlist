# ADR-0001 Frontend Technology Stack Selection

**Author**: Pierre Fouilloux

![Accepted](https://img.shields.io/badge/status-accepted-success) ![Date](https://img.shields.io/badge/Date-10_Feb_2024-lightblue)

## Context and Problem Statement

We need to select a frontend technology stack for a client-side application to combine url allow/block lists and deduplicate them.
It will be hosted on GitHub Pages.
The application needs to handle multi-line text input, file uploads (with client-side storage), and provide syntax highlighting, while maintaining a simple and clean UI.

## Decision Drivers

* Must be 100% client-side with no server dependencies
* Must be deployable to GitHub Pages
* Must handle multi-line text input efficiently
* Must support client-side file storage
* Must have good syntax highlighting capabilities
* Must be maintainable and have a small learning curve
* Must have small bundle size for fast loading

## Considered Options

* Option 1: Vite + Svelte + TailwindCSS + PNPM
* Option 2: Next.js + React + CSS Modules + NPM
* Option 3: Vue CLI + Vue.js + Vuetify + Yarn
* Option 4: Vanilla JS + Bootstrap + NPM

## Decision Outcome

Chosen option: "Vite + Svelte + TailwindCSS + PNPM", because it provides the best balance of performance, developer experience, and maintainability while meeting all our requirements.

### Consequences

* Good, because Vite provides excellent development experience and GitHub Pages deployment
* Good, because Svelte has minimal boilerplate and excellent performance
* Good, because TailwindCSS enables rapid UI development without excess CSS
* Good, because PNPM offers efficient dependency management
* Bad, because the Svelte has a smaller community than React/Vue

### Confirmation

The implementation can be confirmed by:

1. Verifying the bundle size is under 100KB for initial load
2. Running Lighthouse performance tests (target score > 95)
3. Testing offline functionality works as expected
4. Verifying syntax highlighting works in all major browsers
5. Confirming the application works without any backend calls

## Pros and Cons of the Options

### Vite + Svelte + TailwindCSS + PNPM

* Good, because Vite offers the fastest development experience
* Good, because Svelte has zero runtime overhead
* Good, because TailwindCSS results in minimal CSS bundle size
* Good, because PNPM is disk space efficient
* Bad, because Svelte has a smaller ecosystem than React
* Bad, because TailwindCSS requires learning utility classes

### Next.js + React + CSS Modules + NPM

* Good, because React has the largest ecosystem
* Good, because CSS Modules provide good scoping
* Bad, because Next.js includes server-side features we don't need
* Bad, because React has runtime overhead
* Bad, because NPM is less efficient than PNPM

### Vue CLI + Vue.js + Vuetify + Yarn

* Good, because Vue.js is easy to learn
* Good, because Vuetify provides ready-made components
* Bad, because Vuetify adds significant bundle size
* Bad, because Vue CLI is slower than Vite
* Bad, because Yarn doesn't have PNPM's efficiency

### Vanilla JS + Bootstrap + NPM

* Good, because it has zero framework overhead
* Good, because Bootstrap is well-known
* Bad, because more boilerplate code needed
* Bad, because harder to maintain as app grows
* Bad, because less structured development approach

## More Information

* The chosen stack aligns with modern web development practices
* All tools are actively maintained with strong communities
* Stack can be extended later if needed without major refactoring
* Development can start immediately with minimal setup
