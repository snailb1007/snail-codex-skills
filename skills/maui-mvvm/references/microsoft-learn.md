# Microsoft Learn Notes For MAUI MVVM

Use this file when you need the rationale behind the skill rules or need source links for a MAUI MVVM decision.

## Source Links

- [Model-View-ViewModel (MVVM)](https://learn.microsoft.com/en-gb/dotnet/architecture/maui/mvvm)
- [Data binding and MVVM - .NET MAUI](https://learn.microsoft.com/en-us/dotnet/maui/xaml/fundamentals/mvvm?view=net-maui-10.0)
- [Navigation](https://learn.microsoft.com/en-us/dotnet/architecture/maui/navigation)
- [Compiled bindings](https://learn.microsoft.com/en-us/dotnet/maui/fundamentals/data-binding/compiled-bindings?view=net-maui-10.0)

Docs checked: 2026-04-15.

## Distilled Guidance

### Architecture split

- Microsoft positions MVVM as a way to separate UI from presentation and business logic so the app is easier to test, maintain, and evolve.
- The view knows the viewmodel, and the viewmodel knows the model. The model should not know about the viewmodel, and the viewmodel should not know about the view.
- Views in MAUI are typically `ContentPage`, `ContentView`, or `DataTemplate` definitions.

### View rules

- Keep views focused on layout, appearance, and visual behavior.
- Keep code-behind minimal.
- Bind enable/disable state and interaction outcomes to viewmodel properties instead of mutating controls directly in code-behind.
- When interaction starts from an event, behaviors are a valid bridge to invoke a viewmodel command.

### ViewModel rules

- Expose bindable properties and commands.
- Use async operations for I/O and long-running work to keep the UI responsive.
- Implement change notification for bindable state.
- Raise `PropertyChanged` only after the value has actually changed and the object is in a safe, updated state.
- Raise dependent notifications for computed properties when needed.
- Do not raise `PropertyChanged` during constructor-time initialization.
- Use `ObservableCollection<T>` for mutable collections that the UI observes.

### Binding rules

- Every view should end up with a `BindingContext` pointing at its viewmodel.
- `x:DataType` enables compiled bindings and catches bad bindings at build time.
- Re-declare `x:DataType` inside each `DataTemplate`; otherwise the template can inherit an incorrect outer type.
- It is valid to mix compiled and classic bindings deliberately, but do so intentionally.

### Composition

- Microsoft describes both view-first and viewmodel-first composition.
- View-first composition aligns naturally with MAUI navigation because pages are typically constructed by the platform.
- Programmatic `BindingContext` assignment is acceptable when constructor dependencies are required.

### Navigation

- Navigation in MVVM becomes easier to test when it is driven from the viewmodel through a navigation abstraction.
- With Shell-based apps, route registration and route-based navigation are the standard building blocks.
- Navigation parameters can be passed as a dictionary and received by the destination viewmodel via query properties or equivalent initialization hooks.
- Keep navigation logic out of direct view-to-view coupling where practical.

### Practical implication for this skill

- Prefer feature code that flows `View -> ViewModel -> Service/Model`.
- Treat code-behind as an exception layer for UI-only behavior.
- Prefer bindings and commands over event handlers when the control supports them.
- Prefer introducing explicit state properties over hidden UI mutations.
