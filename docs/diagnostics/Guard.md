---
title: Guard
author: Sergio0694
description: Helper methods to verify conditions when running code
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, debug, net core, net standard
dev_langs:
  - csharp
---

# Guard

The [Guard](/dotnet/api/microsoft.toolkit.diagnostics.guard) can be used to validate method arguments in a streamlined manner, which is also faster, less verbose, more expressive and less error prone than manually writing checks and throwing exceptions.

> **Platform APIs:** [`Guard`](/dotnet/api/microsoft.toolkit.diagnostics.guard), [`CallerArgumentExpressionAttribute`](/dotnet/api/system.runtime.compilerservices.callerargumentexpressionattribute)

## How it works

These `Guard` APIs are built with three core principles in mind:

- Being **fast**. To achieve that, all the APIs have been designed to produce as little code as possible in the caller, and each single Guard API will (almost always) be inlined. Furthermore, specialized methods are generated with T4 templates to achieve the most efficient assembly code possible when working with common types (eg. primitive numeric types).
- Being **helpful**. Each `Guard` API produces a detailed exception message that clearly specifies what went wrong, along with additional info (eg. current variable values), when applicable.
- Being **intuitive**. To achieve this, all the `Guard` APIs have expressive and self-explanatory names that make it immediately clear what each API is supposed to do. This shifts the burden of writing checks away from the developers, letting them express conditions using natural language.

## Syntax

Here is a sample method, with some checks being done with explicitly and with manual throw statements:

```csharp
public static void SampleMethod(int[] array, int index, Span<int> span, string text)
{
    if (array is null)
    {
        throw new ArgumentNullException(nameof(array), "The array must not be null");
    }

    if (array.Length >= 10)
    {
        throw new ArgumentException($"The array must have less than 10 items, had a size of {array.Length}", nameof(array));
    }

    if (index < 0 || index >= array.Length)
    {
        throw new ArgumentOutOfRangeException(nameof(index), $"The index must be in the [0, {array.Length}) range, was {index}");
    }

    if (span.Length < array.Length)
    {
        throw new ArgumentException($"The target span is shorter than the input array, had a length of {span.Length}", nameof(span));
    }

    if (string.IsNullOrEmpty(text))
    {
        throw new ArgumentException("The input text can't be null or empty", nameof(text));
    }
}
```

And here is the same method, but using the new `Guard.APIs` to validate the input arguments:

```csharp
public static void SampleMethod(int[] array, int index, Span<int> span, string text)
{
    Guard.IsNotNull(array);
    Guard.HasSizeGreaterThanOrEqualTo(array, 10);
    Guard.IsInRangeFor(index, array);
    Guard.HasSizeLessThanOrEqualTo(array, span);
    Guard.IsNotNullOrEmpty(text);
}
```

The `Guard` APIs will perform the required checks in the fastest way possible, and will throw the appropriate exception with a well formated message if they fail.

> [!NOTE]
> The `Guard` APIs rely on [`[CallerArgumentExpression]`](/dotnet/csharp/language-reference/proposals/csharp-10.0/caller-argument-expression) to automatically infer the name of the argument being validated. This requires C# 10 to be enabled in the project in use. If you're using a lower version of the language, you will need to manually pass the parameter name, for instance using `nameof()` to refer to it (eg. `Guard.IsNotNull(array, nameof(array)))`).

## Methods

There are dozens of different APIs and overloads in the `Guard` class, here are a few of them:

### General

| Methods | Return Type | Description |
| -- | -- | -- |
| IsNotNull&lt;T>(T, string) | void | Asserts that the input value is not null |
| IsOfType&lt;T>(object, string) | void | Asserts that the input value is of a specific type |
| IsAssignableToType&lt;T>(object, string) | void | Asserts that the input value can be assigned to a specified type |
| IsReferenceEqualTo&lt;T>(T, T, string) | void | Asserts that the input value must be the same instance as the target value |
| IsTrue(bool, string) | void | Asserts that the input value must be true |

### Comparisons

| Methods | Return Type | Description |
| -- | -- | -- |
| IsEqualTo&lt;T>(T, T, string) | void | Asserts that the input value must be equal to a specified value |
| IsBitwiseEqualTo&lt;T>(T, T, string) | void | Asserts that the input value must be a bitwise match with a specified value |
| IsLessThan&lt;T>(T, T, string) | void | Asserts that the input value must be less than a specified value |
| IsLessThanOrEqualTo&lt;T>(T, T, string) | void | Asserts that the input value must be less than or equal to a specified value |
| IsInRange&lt;T>(T, T, T, string) | void | Asserts that the input value must be in the [minimum, maximum) range |
| IsBetween&lt;T>(T, T, T, string name) | void | Asserts that the input value must be in the (minimum, maximum) interval |
| IsBetweenOrEqualTo&lt;T>(T, T, T, string name) | void | Asserts that the input value must be in the [minimum, maximum] interval |

### Strings

| Methods | Return Type | Description |
| -- | -- | -- |
| IsNotNullOrEmpty(string, string) | void | Asserts that the input string instance must not be null or empty |
| IsNotNullOrWhitespace(string, string) | void | Asserts that the input string instance must not be null or whitespace |

### Collections

| Methods | Return Type | Description |
| -- | -- | -- |
| IsNotEmpty&lt;T>(T[], string) | void | Asserts that the input array instance must not be empty |
| HasSizeEqualTo&lt;T>(T[], int, string) | void | Asserts that the input array instance must have a size of a specified value |
| HasSizeAtLeast&lt;T>(T[], int, string) | void | Asserts that the input array must have a size of at least or equal to a specified value |
| IsInRangeFor&lt;T>(int, T[], string) | void | Asserts that the input index is valid for a given array |
| HasSizeLessThanOrEqualTo&lt;T>(T[], T[], string) | void | Asserts that the source array must have a size of less than or equal to that of the destination array |

### Tasks

| Methods | Return Type | Description |
| -- | -- | -- |
| IsCompleted(Task, string) | void | Asserts that the input task is in a completed state |
| IsNotCanceled(Task, string) | void | Asserts that the input task is not canceled |

## Examples

You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Diagnostics.UnitTests).
