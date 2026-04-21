# .NET Guidance

## Contents

1. Dependency injection
2. Naming and style
3. Async and cancellation
4. Exceptions
5. Testing
6. Maintainability and analyzers
7. Sources

## Dependency injection

Prefer these defaults:

- Design services to be small, well-factored, and easy to test.
- Treat many injected dependencies as an SRP warning, not as proof that “DI is bad.”
- Avoid direct instantiation of dependent classes inside services when it creates hard coupling.
- Avoid stateful static classes and global mutable state.
- Choose service lifetimes intentionally and keep scoped/transient/singleton usage coherent.

Use an interface when there is a real consuming boundary, replacement need, or testing seam. Do not add an interface only to satisfy a blanket rule.

## Naming and style

Prefer:

- PascalCase for types and members
- camelCase for locals and parameters
- `I` prefix for interfaces
- `Async` suffix for awaitable methods
- Descriptive names over abbreviations

Follow repository conventions when they are already consistent. Do not “clean up” naming in unrelated files just to match personal taste.

## Async and cancellation

Default to TAP for new async APIs.

Prefer:

- `Task` or `Task<T>` for async return types
- `CancellationToken` when the operation can actually honor cancellation
- Non-blocking composition such as `await`, `Task.WhenAll`, and `Task.WhenAny`

Avoid:

- `async void` outside event handlers
- Sync-over-async patterns such as `.Result` and `.Wait()`
- Exposing cancellation tokens that the implementation ignores

Consider `ValueTask` only for performance-sensitive hot paths where you understand the tradeoffs.

## Exceptions

Use exceptions for exceptional conditions, not normal control flow.

Prefer:

- Catch only when you can recover, translate, or add meaningful context
- Preserve stack traces with `throw;`
- Domain-appropriate exception types at boundaries

Avoid broad catch blocks that silently swallow failures.

## Testing

Keep unit tests:

- Fast
- Independent
- Repeatable
- Focused on one behavior

Use Arrange-Act-Assert or an equally clear structure. Prefer tests around observable behavior instead of implementation details.

When refactoring for SOLID, use tests to lock behavior before widening the seam.

## Maintainability and analyzers

Use Roslyn analyzers and code-style rules as a guardrail, not as a replacement for design judgment.

Pay attention to:

- Maintainability warnings
- Unnecessary code rules
- Naming/style consistency
- Async and exception quality rules

Analyzer pressure is a signal. Confirm that the fix improves the design instead of merely satisfying the rule.

## Sources

Primary sources used for this skill:

- Dependency injection guidelines: https://learn.microsoft.com/dotnet/core/extensions/dependency-injection/guidelines
- Dependency injection overview: https://learn.microsoft.com/dotnet/core/extensions/dependency-injection/overview
- Service lifetimes: https://learn.microsoft.com/dotnet/core/extensions/dependency-injection/service-lifetimes
- C# identifier naming rules and conventions: https://learn.microsoft.com/dotnet/csharp/fundamentals/coding-style/identifier-names
- Task-based Asynchronous Pattern (TAP): https://learn.microsoft.com/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap
- Async return types (C#): https://learn.microsoft.com/dotnet/csharp/asynchronous-programming/async-return-types
- Handling and throwing exceptions in .NET: https://learn.microsoft.com/dotnet/standard/exceptions/
- CA2200 rethrow guidance: https://learn.microsoft.com/dotnet/fundamentals/code-analysis/quality-rules/ca2200
- Testing in .NET: https://learn.microsoft.com/dotnet/core/testing/
- Best practices for writing unit tests: https://learn.microsoft.com/dotnet/core/testing/unit-testing-best-practices
- MSTest design rules: https://learn.microsoft.com/dotnet/core/testing/mstest-analyzers/design-rules
- Maintainability warnings: https://learn.microsoft.com/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings
- Code-style language rules: https://learn.microsoft.com/dotnet/fundamentals/code-analysis/style-rules/language-rules
- Roslyn analyzers overview: https://learn.microsoft.com/visualstudio/code-quality/roslyn-analyzers-overview?view=vs-2022
- Framework Design Guidelines: https://learn.microsoft.com/dotnet/standard/design-guidelines/
