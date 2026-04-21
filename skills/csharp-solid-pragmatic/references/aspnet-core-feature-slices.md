# ASP.NET Core Feature Slices

## Contents

1. Default slice shape
2. Controller boundaries
3. Application service boundaries
4. Repository boundaries
5. When not to add a layer
6. Refactor heuristics

## Default slice shape

For a typical ASP.NET Core feature, prefer a simple slice:

- Controller or endpoint handles HTTP concerns
- Use-case coordinator or application service handles orchestration
- Domain collaborators handle business rules
- Infrastructure adapters handle persistence, messaging, and external systems

Do not force every feature to have every layer. Add only the boundaries the use case needs.

## Controller boundaries

Controllers should usually own:

- Transport concerns
- Model binding
- HTTP status mapping
- Authorization attributes or endpoint policy hooks

Controllers should usually not own:

- Non-trivial business rules
- Persistence logic
- Email, queue, or external API orchestration details
- Cross-cutting validation beyond simple request-shape checks

If a controller method keeps growing, move orchestration into a focused use-case class before introducing more framework patterns.

## Application service boundaries

An application service or use-case handler is a good place for:

- Coordinating domain steps
- Calling repositories or gateways
- Managing transaction-like ordering of work
- Translating infrastructure output into use-case results

It is a poor place for:

- HTTP-specific logic
- ORM-specific query details everywhere
- Giant “manager” classes that accumulate unrelated workflows

Keep services aligned to use cases or cohesive workflow families, not to technical buckets alone.

## Repository boundaries

Introduce a repository or persistence abstraction when:

- The domain/application layer should not know the storage mechanism
- Persistence is a stable boundary
- Tests benefit from isolating storage behavior

Do not introduce a generic repository just because a template or architecture diagram says so.

Prefer:

- Feature-focused query/command abstractions
- Domain-meaningful operations
- Letting infrastructure own ORM details

Avoid:

- Thin wrappers around `DbSet<T>` with no added semantic value
- A repository layer that exists only to satisfy ceremony

## When not to add a layer

Keep the design flatter when:

- The feature is simple CRUD with minimal policy
- The controller is still small and readable
- The only “service” would be a pass-through wrapper
- A repository abstraction would only duplicate obvious EF Core operations

In those cases, prefer a smaller refactor such as extracting a validator, domain helper, or query object.

## Refactor heuristics

Use these quick choices:

- Fat controller with mixed orchestration:
  extract a use-case/service first.
- Service with mixed policy families:
  split by workflow or rule set before adding patterns.
- Repeated branching by type/status/channel:
  consider strategy objects.
- Many collaborators because of unrelated work:
  split responsibilities before adding more DI.
- Persistence details leaking upward:
  tighten the infrastructure boundary.
