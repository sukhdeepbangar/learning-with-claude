# Java 8 and Beyond: Learning Plan

A structured path through modern Java features, from Java 9 to Java 21+.

---

## Current Status

**Phase:** Not started
**Current topic:** TBD
**Last session:** -

### Where We Left Off

_Starting fresh_

---

## Learning Profile

| Aspect | Preference |
|--------|------------|
| Goals | Learn modern Java features beyond Java 8 |
| Format | IJava notebooks for exploration (to be set up) |
| Focus areas | Syntax changes, concurrency (Virtual Threads), pattern matching |

---

## Phase 1: Quick Wins (Java 9-11)

Small but useful changes that are easy to adopt.

### Topics

- [ ] **Collection factory methods** (Java 9)
  - `List.of()`, `Set.of()`, `Map.of()`
  - Immutable collections

- [ ] **`var` keyword** (Java 10)
  - Local variable type inference
  - When to use, when not to

- [ ] **New String methods** (Java 11)
  - `isBlank()`, `lines()`, `strip()`, `repeat()`

- [ ] **Single-file execution** (Java 11)
  - Run `java MyFile.java` directly, no compile step

---

## Phase 2: Language Enhancements (Java 14-17)

Bigger syntax changes that change how you write Java.

### Topics

- [ ] **Switch expressions** (Java 14)
  - Arrow syntax, yield, returning values

- [ ] **Text blocks** (Java 15)
  - Multi-line strings with `"""`

- [ ] **Records** (Java 16)
  - Immutable data classes with minimal boilerplate
  - When to use vs regular classes

- [ ] **Sealed classes** (Java 17)
  - Controlling inheritance hierarchies

- [ ] **Pattern matching for instanceof** (Java 16)
  - No more casting after instanceof check

---

## Phase 3: Pattern Matching Deep Dive (Java 17-21)

Pattern matching evolves across versions.

### Topics

- [ ] **Pattern matching in switch** (Java 21)
  - Type patterns, guarded patterns

- [ ] **Record patterns** (Java 21)
  - Destructuring records in patterns

- [ ] **Practical patterns**
  - Combining patterns for real-world use cases

---

## Phase 4: Concurrency Revolution (Java 21)

Virtual Threads change everything about Java concurrency.

### Topics

- [ ] **Virtual Threads basics**
  - What they are, why they matter
  - Platform threads vs virtual threads

- [ ] **Creating virtual threads**
  - `Thread.ofVirtual()`, executors

- [ ] **Structured concurrency** (preview)
  - Managing groups of tasks
  - Error handling across concurrent tasks

- [ ] **Scoped values** (preview)
  - Thread-local alternative for virtual threads

### Project: Concurrency Comparison

- [ ] **Build comparison demos**
  - Same task with platform threads vs virtual threads
  - Measure and observe differences

---

## Phase 5: Other Notable Features

Pick based on interest.

- [ ] **Modules** (Java 9) - Project Jigsaw
- [ ] **HTTP Client** (Java 11) - Modern HTTP API
- [ ] **Foreign Function & Memory API** (Java 21) - Native interop
- [ ] **Sequenced Collections** (Java 21) - Ordered collection interfaces

---

## Setup

### JShell (built-in, Java 9+)

Quick syntax exploration:
```bash
jshell
```

### IJava Notebooks (recommended)

For documented, committable exploration:
- Repository: https://github.com/SpencerPark/IJava
- Setup guide: _to be added_

---

## Session Log

| Date | Phase | Topics Covered | Notes |
|------|-------|----------------|-------|

---

## Resources Created

| Resource | Type | Phase | Link |
|----------|------|-------|------|

