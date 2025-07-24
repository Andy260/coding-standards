# General Guidelines

This document describes the general conventions and coding styles that should be followed within my personal projects.

[TOC]

## Language Specific

Each language used in this project have specific style rules and guidelines, and while the guides may not be comprehensive, the general guidelines should be followed in cases where the style document doesn't cover the specific circumstance.

- [C#](Languages/C-Sharp.md)
- [C++](Languages/C-PlusPlus.md)
- [CSS](Languages/CSS.md)
- [HTML](Languages/HTML.md)
- [Markdown](Languages/Markdown.md)
- [Razor](Languages/Razor.md)
- [Rust](Languages/Rust.md)
- [Sass (SCSS)](Languages/SCSS.md)
- [Typescript](Languages/Typescript.md)

## Formatting

This section covers topics relating to the formatting of source files within the project.

### Use Australian English

When naming variables/functions/methods/etc, writing documentation, or writing in general within the project, use Australian English.

### Character Line Limit

All documents should follow a 180 character line limit unless an exception is made within the language's respective coding style document.

This can be enforced in many IDEs:

- [Visual Studio Code](https://stackoverflow.com/questions/29968499/how-can-i-have-multiple-vertical-rulers-in-vs-code)
- [Visual Studio](https://stackoverflow.com/questions/60060373/in-visual-studio-code-how-to-extend-the-maximum-line-width)
- [JetBrains Rider](https://stackoverflow.com/questions/24355976/how-to-change-line-width-in-intellij-from-120-character)

### Use Automated Formatting Tools

Adopt code formatters (e.g., Prettier for TypeScript, clang-format for C++, dotnet-format for C#) to ensure consistent style.

```markdown
Configure your IDE to format code on save using the project's preferred tool.
```

## Errors

This section describes how warning and/or errors should be handled within the project.

### Compilation Warnings And Errors

In languages which support throwing of warnings and/or errors, this section describes how they should be handled within this project.

### Use Highest Level Warnings

The highest level of warnings and/or errors should be used. This ensures that as many language level bugs can be caught during compilation rather than runtime. Exceptions can be made to this rule, only when absolutely necessary or with good reason.

### Treat Warnings As Errors

Warnings should be resolved and treated as errors before the code is makes it into production as they could be indicating unfixed bugs as well as potentially poorly written code.

## Documentation

This section covers topics relating to the documentation of the project's usage, and code documentation (source file comments, API documentation, etc).

### Write Accessible and Clear Documentation

Use Markdown for documentation, provide alt text for images, and use clear language.

```markdown
![Screenshot showing the settings menu](/images/settings.png)
```

```html
<!-- Do -->
<img src="/images/settings.png" alt="Screenshot showing the settings menu">

<!-- Don't -->
<img src="/images/settings.png">
```

### Write Clear and Concise Comments

Use comments to explain complex logic, assumptions, or important decisions. Avoid redundant comments.

```cpp
// Do
// Calculates the factorial of n recursively.
int factorial(int n) { ... }

// Don't
// This is a function
int factorial(int n) { ... }
```

```rust
// Do
/// Returns the sum of all elements in the slice.
fn sum(slice: &[i32]) -> i32 { ... }
```

### Write Descriptive Commit Messages

Use clear, concise commit messages that explain the intent of the change.

```markdown
// Do
Add input validation to user registration form

// Don't
Fix stuff
```

### Document Public APIs and Modules

Provide documentation for public-facing APIs, modules, and complex logic to help other developers understand usage and intent.

```csharp
/// <summary>
/// Calculates the factorial of a number.
/// </summary>
public int Factorial(int n) { ... }
```

```typescript
/**
 * Returns the sum of all elements in the array.
 */
function sum(arr: number[]): number { ... }
```

```rust
/// Returns the sum of all elements in the slice.
fn sum(slice: &[i32]) -> i32 { ... }
```

## Maintainability

This section focuses on topics relating to the maintainability of the code base.

### Avoid Magic Numbers and Strings

Use named constants instead of unexplained literals to improve readability and maintainability.

```csharp
const int MaxRetries = 5;
if (retries > MaxRetries) { ... }
```

```typescript
const MAX_RETRIES = 5;
if (retries > MAX_RETRIES) { ... }
```

### Prefer Early Returns to Reduce Nesting

Minimise deep nesting by using early returns or guard clauses.

```csharp
void Process(User user)
{
    if (user == null) return;
    // ...rest of logic...
}
```

```typescript
function process(user?: User) {
    if (!user) return;
    // ...rest of logic...
}
```

### Keep Dependencies Up To Date

Regularly update dependencies and remove unused ones to reduce security risks and maintenance burden.

```markdown
Run dependency update checks before major releases.
```

### Practice Secure Coding

Validate all inputs, avoid hardcoded secrets, and follow security best practices for the language and framework.

```csharp
// Do
var password = Environment.GetEnvironmentVariable("APP_PASSWORD");

// Don't
var password = "supersecret";
```

```typescript
// Do
const apiKey = process.env.API_KEY;

// Don't
const apiKey = "hardcoded-key";
```

### Project Testing

Unless otherwise specified, each project should have some kind of testing suite (where possible or applicable). This ensures a general level of expected behaviour can be expected from the project.

### Don't Reimplement Standard Library Functionality

Most languages tend to provide a standard library of some kind which contains functionality which is generally helpful and desirable in a lot of general use cases, and as such shouldn't be reimplemented.

There are situations where reimplementing such functionality is desirable and even encourages, such as when binary size is important on embedded systems, standard library contains error prone implementations or doesn't meet the performance targets of the project.

But in general, the standard library should be strongly preferred.

### Keep Source Files Reasonable In Size

Over time source files can grow in size and while this is generally expected, care should be taken to ensure the file growth is reasonable. Each language have their own quirks, but in general if it feels like the source file is becoming harder to follow or maintain, it may be time to split the file up into separate modules.

### Ensure Modules Are Singular Purpose

A common mistake when designing modules within most languages (such as classes and/or structure in C style languages) is giving one module too much responsibility. This leads to large source files that are hard to follow and tend to be too complex. The best remedy to such situations is splitting up such monolithic modules into separate small modules which all complete small tasks of the bigger task.
