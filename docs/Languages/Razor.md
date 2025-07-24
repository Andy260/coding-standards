# Razor Coding Style

This documents describes the conventions and styling used when contributing Razor code to this project (`.razor` and `.cshtml` files).

All embedded HTML code in `.razor` files should conform to both the guidance provided in this document and the dedicated [HTML](HTML.md) coding style document.

In addition to the styles and conventions outlined in this document, the general guidelines outlined within the [GeneralGuidelines.md](../GeneralGuidelines.md) document should also be followed.

[TOC]

## Layout

Razor documents should follow the following order:

- `@page` (if required)
- `@layout` (optional)
- `@rendermode` (optional)
- `@attribute` directives (if required)
- `@inherit` directive (if required)
- `@implements` directives (if required)
- `@inject` directives (if required)
- `@typeparam` directives (if required)
- `@using` directives (if required)
- Head content (if required)
- Page content
- `@code` in Razor components or `@functions`

```cshtml
@* Page directive *@
@page /
@* Layout directive *@
@layout MainLayout
@* Render mode *@
@rendermode InteractiveServer

@* Attributes, inheritance, interface implementations, injections, type parameters *@
@attribute [StreamRendering]
@inherits BaseClass
@implements IDisposable
@typeparam TEntity
@inject ILogger<Counter1> Logger

@* Namespace usings *@
@using Microsoft.AspNetCore.Components.Web

@* Head content *@
<PageTitle>Hello World!</PageTitle>

@* Page content *@
<p>Hello World!</p>

@code {
  // Component code
  ...
}
```

## Razor Comments

When commenting Razor documents only use the Razor delimited syntax rather than C# comments or HTML comments. And ensure single line comments only occupy one line in the source code, and multi-line comments are wrapped by the `@* *@` delimiters surround them.

```cshtml
@* Single line comment *@

@*
  Multi
  line
  comment.
*@
```

## Prefer `@code` Over `@function` In Components

When implementing a Razor component, prefer using the `@code` directive define relevant C# code over using the `@function` directive.

```cshtml
@* Do *@
@code {
  ...
}

@* Don't *@
@functions {
  ...
}
```

## C# Expressions And Code

All C# code and expressions within Razor files should conform to the [C#](C-Sharp.md) coding style guide.

## Tags Usage

This section describes how tags should be used within Razor documents.

### Always Quote Attribute Values

When quoting attribute values, ensure to use quotations.

```cshtml
@* Do *@
<MyComponent Value="@Value" /> 
@* Don't *@
<MyComponent Value=@Value /> 
```

### Close Empty Elements

While Razor components without any inner content can be closed with a closing tag, such definitions should be closed with a `/` rather than a closing tag.

```cshtml
@* Do *@
<NavMenu /> 

@* Don't *@
<NavMenu></NavMenu>
```

## Styling

Inline styling should be avoided as much as possible, preferring styling defined in `.scss` files. And styles used by multiple components or parts of the application should be written in their own separate `.scss` file, and with per-component styling written in `.scss` files which use css isolation.

For example: `App.razor` and `App.scss` (compiled to `App.css`) for global styles, and `MyComponent.razor` with `MyComponent.scss` (compiled to `MyComponent.css`) for component only styling.

```text
.
├── App.razor
├── App.scss
└── Components/
    ├── MyComponent.razor
    └── MyComponent.razor.scss
```

## JavaScript Interop

When writing code for JavaScript interop (implementing functionality that cannot be done within `.razor` files), writing the code within Typescript is strongly preferred. 

The Typescript file should be written as an isolated `.ts` file within a `.razor` component.

```text
└── Components/
    ├── MyComponent.razor
    └── MyComponent.razor.ts
```

And the code within the isolated `.ts` file should be written within an `export` function which is executed within the `.razor` component. The code within the isolated Typescript file should also use JSDOc style comments to ensure the expected usage is clear. In addition to this, all Typescript code written should following the guidelines and style as outlined in the [Typescript.md](Typescript.md) document.

```typescript
/**
 * Does some work
 * @param number The amount of work to do.
 * @returns void
 */
export function doWork(number: int) : void
{
    // Do something
}
```

In such cases where the functionality provided the Typescript code is used within multiple components, execution of the Typescript code should still be done with a dedicated C# `class` or `.razor` component.

```csharp
/// <summary>
/// A component which does some work within JavaScript.
/// </summary>
public class MyComponent
{
    private IJSObjectReference? _module;

    /// <summary>
    /// Constructs a new instance of this object and loads the JavaScript code.
    /// </summary>
    public MyComponent()
    {
        _module = await JSRuntime.InvokeAsync<IJSObjectReference>("import", 
                "./Components/MyComponent.razor.js");
    }

    /// <summary>
    /// </summary>
    /// <param name="number">The amount of work to do.</param>
    /// <returns>A task representing the asynchronous operation.</returns>
    public async Task DoSomeWork(int number)
    {
        if (_module is not null)
        {
            await _module.InvokeVoidAsync("doWork", number);
        }
    }
}
```

## HTML Comments

While Razor comments should be preferred, if HTML comments in the output HTML is desired, ensure single line comments only occupy one line in the source code, and multi-line comments are wrapped by the `<!--` `-->` tags surround them.

```html
<!-- Single line comment -->

<!--
  Multi
  line
  comment.
-->
```
