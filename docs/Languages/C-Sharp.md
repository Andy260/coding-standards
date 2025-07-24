# C# Coding Style

This documents describes the conventions and styling used when writing C# code.

These styles and conventions are inspired by Microsoft's [identifier naming rules and conventions][csharp-naming] and [coding style][csharp-codingstyle], as well as [dofactory's coding style](https://www.dofactory.com/csharp-coding-standards), in addition to my own conventions and styles which I have used over the years.

[csharp-naming]: https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/identifier-names
[csharp-codingstyle]: https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions

[TOC]

## Naming Conventions

### Variables

Use camelCasing for local variables and method parameters.

```csharp
public class MyClass
{
    public void DoStuff(int firstArgument)
    {
        int myVar = firstArgument + 1;
    }
}
```

Private variables should be named by being prefixed with an underscore followed by camelCasing.

```csharp
public class SomeClass
{
    private int _memberVar;
}
```

Constants should use PascalCase regardless of their visibility.

```csharp
public const int Width      = 100;
private const string Name   = "My Name";
```

Properties which access private variables or auto properties should be preferred over Public/Internal/Protected variables, so the data they access can be controlled.

```csharp
// Do
public bool IsEnabled 
{ 
    get => _isEnabled;
    set
    {
        // Do some checks...
        _isEnabled = value;
    }
}
private bool _isEnabled;
// Or
public int Counter { get; private set; }
// Don't
public string Name;
```

### Namespaces

Use PascalCase, and organise namespaces with a clearly defined structure, with their intended usage and/or components contained within clear from the name used.

```csharp
namespace MyProject.Components.Module
namespace MyProject.Server.Lobbies
```

### Interfaces

Prefix interface names with `I` and use PascalCase.

```csharp
public interface ISomeInterface
{
    ...
}
```

### Methods

Use PascalCase when naming methods, and prefer names which clearly define their usage and purpose.

Examples:

- `NotifyUsers(string message)`
- `Player.CalculatePoints()`
- `Lobby.Close()`

```csharp
public void SomeMethod(int firstArgument, int secondArgument)
{
    ...
}
```

### Properties

Use PascalCase.

```csharp
public bool IsEnabled { get; private set; }
```

## Layout

### Indentation And Spacing

- Use 4 spaces per indentation level. Do not use tabs.
- Place a single space before and after operators.
- Place a single blank line between method definitions and property definitions.

### Braces Usage

Use [Allman](https://en.wikipedia.org/wiki/Indentation_style#Allman_style) Style braces.

```csharp
public void MyFunction()
{
    ...
}
```

### Line Length

- Keep lines under 80 characters.
- Wrap long lines when necessary.

### Blank Lines

Use blank lines to separate logical sections of the code.

```csharp
public class ExampleClass
{
    private int _count;

    public void Increment()
    {
        _count++;
    }

    public int GetCount()
    {
        return _count;
    }
}
```

### Order Of Members

Organise members in the following order:

1. Constants
2. Fields
3. Constructors
4. Properties
5. Methods

```csharp
public class ExampleClass
{
    public const int MaxValue = 100;
    private int _count;

    public ExampleClass(int initialCount)
    {
        _count = initialCount;
    }

    public int Count
    {
        get { return _count; }
        set { _count = value; }
    }

    public void Increment()
    {
        _count++;
    }

    public int GetCount()
    {
        return _count;
    }
}
```

## Language Usage

### Comments Usage

Use XML comments for `public` and `protected` members, and use all appropriate tags (such as argument/exception tags).

```csharp
/// <summary>
/// Buys a new Car.
/// </summary>
/// <param name="model">The model of Car to buy.</param>
/// <returns>The recently bought Car.</returns>
public Car BuyCar(CarModel model)
{
    // Do some work...
    return new Car(model);
}
```

### `var` usage

Avoid using `var` as much as possible. While IDEs can normally provide the used type, there are times when the IDE may not be able to properly infer the intended type or the code may be shown within a snippet where an IDE would not be available for such purposes, so being explicit in your intentions is preferred. The exception to this rule, is when it will improve readability.

```csharp
// Do
int number = 10;

// Don't
var number = 10;
```

### Properties Usage

Prefer auto properties where appropriate. Don't use properties with a similar access modifier on both the `get` `set` as this may indicate poor design.

```csharp
// Do - auto properties
public string Name { get; private set; }

// Do
private int _myCounter;
public int MyCounter 
{
    get => _myCounter;
    set
    {
        // Do some checks...
        _myCounter = value;
    }
}

// Don't - shows bad design
public bool ShouldDeploy { get; set; }
```

### `if` Statements

When declaring an if statement with only one line within its code block, braces should be still used to ensure any additional code added will be executed within the code block.

```csharp
// Do
if (person.age > 18)
{
    person.type = PersonType.Adult;
}

// Don't
if (person.age > 18)
    person.type = PersonType.Adult;
```

### LINQ Usage

When using LINQ, use the method syntax over the query syntax as it is preferred by the community and can be easier to read, so it doesn't look out of place in the syntax of the C# language.

```csharp
// Do - Method syntax
IEnumerable<int> orderingQuery = 
    numbers.Order().
    Select(num => num < 3 || num > 7)

// Don't - Query syntax
IEnumerable<int> orderingQuery =
    from num in numbers
    where num is < 3 or > 7
    orderby num ascending
    select num;
```

### `switch` Usage

When declaring `switch` statements which use an `enum` for their condition, ensure to write a `default` case which throws a `NotImplementedException` exception in the case that the `enum` has an additional state and the `switch` statement hasn't yet been updated to consider it.

```csharp
switch (state)
{
    case State.First:
        break;

    case State.Second:
        break;

    default:
        throw new NotImplementedException($"{nameof(state)} not implemented");
}
```

### Error Handling

#### Exceptions

- Use exceptions for error conditions, not for regular control flow.
- Throw specific exceptions.
- Always include a meaningful message.

```csharp
if (value < 0)
{
    throw new ArgumentOutOfRangeException(nameof(value), "Value cannot be negative.");
}
```

#### `try` - `catch` Blocks

- Catch specific exceptions whenever possible.
- Avoid empty catch blocks.
- Log exceptions or handle them appropriately.

```csharp
try
{
    // Code that may throw
    ...
}
catch (IOException exception)
{
    // Handle IOException
    _logger.LogError(exception, "Unable to write to file");
}
catch (Exception exception)
{
    // Handle other exceptions
    _logger.LogError(exception, "Unknown error");
    throw;
}
```

### `string` construction

Prefer constructing strings using interpolation over concatenation.

```csharp
string name     = "John";
int age         = 30;

// Do - interpolation
string message = $"Name: {name}, Age: {age}";

// Don't - concatenation
string message = "Name: " + name + ", Age: " + age;
```

### `async` / `await`

- Use `async` and `await` for asynchronous programming.
- Use `Task` for methods that perform asynchronous operations.

```csharp
public async Task LoadDataAsync()
{
    ServerData data = await FetchDataFromServerAsync();
    // Process data
}
```

### `null` Checking

- Use the null-coalescing operator `??` and null-conditional operator `?.`.

```csharp
string message  = input ?? "Default message";
int? length     = input?.Length;
```

### Events Publishing

Publish events which confirm to the [.NET Guidelines](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines).

```csharp
// Event with custom data
public sealed class CustomEventArgs : EventArgs
{
    public CustomEventArgs(string message)
    {
        Message = message;
    }

    public string Message { get; private set; }
}

public sealed class Publisher
{
    public event EventHandler<CustomEventArgs>? RaiseCustomEvent;

    public void DoSomething()
    {
        EventHandler<CustomEventArgs>? raiseEvent = RaiseCustomEvent;

        if (RaiseCustomEvent != null)
        {
            RaiseCustomEvent?.Invoke(this, new CustomEventArgs("Something happened!"));
        }
    }
}

// Events without custom data
public sealed class Publisher
{
    public event EventHandler? RaiseCustomEvent;

    public void DoSomething()
    {
        EventHandler? raiseEvent = RaiseCustomEvent;

        if (RaiseCustomEvent != null)
        {
            RaiseCustomEvent?.Invoke(this, EventArgs.Empty);
        }
    }
}
```

## Miscellaneous

### File Organisation

- Place each class/structure/enum/etc in it's own file.
- Name the file after the object it contains.

### Regions

- Use regions to organise code into sections.
- Do not overuse regions; prefer logical grouping of related code.

```csharp
#region Public Methods

public void Method1()
{
    ...
}

#endregion
```
