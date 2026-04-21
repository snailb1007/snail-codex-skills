# Pragmatic Review Checklist

## Contents

1. Use this checklist
2. Smells by principle
3. Overengineering gate
4. Refactor shapes

## Use this checklist

Before proposing a redesign, answer these questions:

1. What concrete change pressure exists today?
2. What is the smallest change that removes the pressure?
3. What behavior must remain stable?
4. What new abstraction is justified by a boundary, variant, or test seam?
5. What abstraction would merely make the code look “architected”?

Before discussing patterns, also check:

- Is there a correctness bug hidden inside the design smell?
- Is there a normalization, concurrency, or data-integrity problem that matters more than the abstraction discussion?

## Smells by principle

### SRP smells

- One class owns validation, mapping, persistence, notification, and logging.
- A service has a long constructor and many unrelated collaborators.
- A method mixes orchestration with domain calculations and presentation formatting.

### OCP smells

- Business policy grows through repeated `switch` or `if/else` chains.
- New variants require editing several existing files in the same layer.
- Feature flags are used to emulate separate strategies for long periods.

### LSP smells

- Child types throw for inherited methods that callers reasonably expect to work.
- Base assumptions no longer hold for derived types.
- Consumers need `if (x is DerivedType)` checks to stay safe.

### ISP smells

- An interface forces methods or properties that some implementers cannot use meaningfully.
- Consumers inject a broad interface but only use one small slice of it.
- DTO-like or library-style “all in one” interfaces leak everywhere.

### DIP smells

- Application code directly constructs gateways, HTTP clients, repositories, or email senders.
- Business logic reads global singletons or static state.
- A class is hard to test because infrastructure is baked into the method body.

## Overengineering gate

Stop and simplify when you see this pattern:

- Interface added for one implementation with no meaningful seam
- Generic repository or service layer added with no domain-specific behavior
- Factory or strategy introduced before a second real variant exists
- Deep inheritance used where role composition would be clearer
- Too many tiny files that hide a simple use case instead of clarifying it

Use these pragmatic defaults:

- Prefer concrete classes inside a local feature until a seam is needed.
- Prefer extracting a focused class before introducing a framework pattern.
- Prefer deleting indirection over preserving it for hypothetical reuse.

## Refactor shapes

Use these common moves:

- Split orchestration from policy:
  keep the use-case coordinator thin and move business rules into focused collaborators.
- Replace conditionals with strategies:
  do this only when behavior families must vary independently or keep growing.
- Replace inheritance with roles:
  use focused interfaces when the subtype relation is unstable.
- Introduce boundary abstractions:
  apply this at infrastructure edges such as persistence, messaging, clock, or external APIs.
- Shrink broad interfaces:
  split by consumer need, not by arbitrary technical categories.
