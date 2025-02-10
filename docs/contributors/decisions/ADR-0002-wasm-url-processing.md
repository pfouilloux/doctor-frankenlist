# ADR-0002 URL Processing Implementation in Rust + WASM

**Author**: Pierre Fouilloux

![Proposed](https://img.shields.io/badge/status-proposed-yellow) ![Date](https://img.shields.io/badge/Date-10_Feb_2024-lightblue)

## Context and Problem Statement

The application needs to process, parse, deduplicate, and reformat URL lists efficiently. This operation can become CPU-intensive with large lists and requires careful memory management. We need to decide whether to implement this functionality in TypeScript or delegate it to a WASM module written in Rust.

## Decision Drivers

* Processing performance for large URL lists
* Memory efficiency when handling large datasets
* Code reusability across web and CLI interfaces
* Development and maintenance complexity
* Bundle size impact
* Browser compatibility requirements
* Development team expertise requirements

## Considered Options

* Option 1: Rust + WASM library with CLI companion
* Option 2: Pure TypeScript implementation
* Option 3: Hybrid approach (TypeScript with WASM for specific operations)
* Option 4: Go + WASM implementation

## Decision Outcome

Chosen option: "Rust + WASM library with CLI companion", because it offers the best performance characteristics while enabling code reuse between web and CLI interfaces.

### Consequences

* Good, because Rust provides memory safety and high performance
* Good, because code can be shared between web and CLI versions
* Good, because WASM enables near-native performance in the browser
* Good, because Rust's type system catches errors at compile time
* Bad, because it adds complexity to the build process
* Bad, because it requires Rust expertise in the team
* Bad, because it increases the initial development time

### Confirmation

The implementation can be confirmed by:
1. Performance benchmarks showing >5x improvement over TypeScript for lists with >1000 URLs
2. Memory usage tests showing efficient handling of large datasets
3. Successful compilation and running of the same code in both WASM and CLI contexts
4. Browser compatibility tests across major browsers
5. Bundle size impact remaining under 250KB for the WASM module

## Pros and Cons of the Options

### Rust + WASM library with CLI companion

* Good, because Rust offers best-in-class performance
* Good, because single codebase for web and CLI
* Good, because strong type system prevents runtime errors
* Good, because excellent memory safety guarantees
* Bad, because requires Rust knowledge
* Bad, because adds build complexity
* Bad, because increases initial development time

### Pure TypeScript implementation

* Good, because simpler development workflow
* Good, because matches existing frontend stack
* Good, because easier to debug in browser
* Bad, because potentially slower performance
* Bad, because requires separate CLI implementation
* Bad, because less memory efficient
* Bad, because more prone to runtime errors

### Hybrid approach

* Good, because balances complexity and performance
* Good, because allows gradual migration to WASM
* Good, because keeps simple operations in TypeScript
* Bad, because maintains two codebases
* Bad, because increases architectural complexity
* Bad, because harder to maintain consistency

### Go + WASM implementation

* Good, because simpler than Rust
* Good, because good performance characteristics
* Bad, because larger WASM bundle size than Rust
* Bad, because less mature WASM tooling
* Bad, because requires another language expertise

## More Information

* WASM modules should be loaded asynchronously to not block the main thread
* Consider using web workers for processing large lists
* Implementation should follow the builder pattern for flexible URL processing pipelines
* Consider implementing streaming processing for very large lists
* Plan to add benchmarking suite to track performance
