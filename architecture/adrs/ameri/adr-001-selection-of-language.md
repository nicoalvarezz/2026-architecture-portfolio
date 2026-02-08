# ADR 001: Selection of Language for `AmeriDB`

**Status:** Accpeted
**Date:** 2026-02-08

## Context

Building a crash-safe, page-based B+Tree storage engine requires a language that provides:

- *Predictable Memory Management*: We need control when bytes are written to the buffer pool and disk. Large Garbage
Collection (GC) pauses can interfere with the database performance benchmarks.
- **Low-Level I/O**: Easy to `pwrite`, `preod`, and `fsync` syscalls.
- **String Typing**: To manage complex binary structures (Pages, WAL entries) without runtime type errors.

## Decision

We will be using **Rust** for the implementation of `AmeriDB`.

### Rationale

1. **Memory Safety**: Database engines are prone to "use-after-free" bugs in buffer management. Rust eliminates this at compile time.
2. **Career Growth**: Aligns with the industry trend toward Rust systems programming.
3. **Mastery**: Using a concrete, complex project (B+Tree) as a vehicle to finally overcome rusts learning curve.

## Alternatives Considered

Other programming languages considered:

- Go: Fast development; great concurrency primitives (goroutines); built-in testing. However, GC can be non-deterministic for low-level buffer management; lacks manual memory control without unsafe.
- C++: The industry standard for DBs (Postgres, MySQL); absolute control over memory and hardware. However, manual memory management leads to segfaults and leaks; building a modern project structure is tedious.

## Consequences

- **Learning Overhead**: We acknowledge that the development will be slower initially.
- **Mitigation**: We will focus on **functional logic over idiomatic perfection** in Q1.
- **Architecture over Syntax**: If Rust concept is too frustrating,
we will document the "Design" first in the Portfolio (Markdown) and return to the code later.
