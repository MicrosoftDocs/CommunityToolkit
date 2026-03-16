---
title: SpanOwner\<T>
author: Sergio0694
description: A stack-only buffer type renting memory from a shared pool
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, parallel, high performance, net core, net standard
dev_langs:
  - csharp
---

# SpanOwner\<T> class

The [`SpanOwner<T>`](/dotnet/api/microsoft.toolkit.highperformance.buffers.spanowner-1) class is a stack-only buffer type that rents buffers from a shared memory pool. It essentially mirrors the functionality of [`MemoryOwner<T>`](/dotnet/api/microsoft.toolkit.highperformance.buffers.memoryowner-1), but as a `ref struct` type. This functionality is particularly useful for short-lived buffers that are only used in synchronous code (that don't require [`Memory<T>`](/dotnet/api/system.memory-1) instances), as well as code running in a tight loop. Creating `SpanOwner<T>` values doesn't require memory allocations.

> **Platform APIs:** [`SpanOwner<T>`](/dotnet/api/microsoft.toolkit.highperformance.buffers.spanowner-1), [`MemoryOwner<T>`](/dotnet/api/microsoft.toolkit.highperformance.buffers.memoryowner-1)

## Syntax

The same core features of `MemoryOwner<T>` apply to this type as well, with the exception of it being a stack-only `struct`. It also lacks the [`IMemoryOwner<T>`](/dotnet/api/system.buffers.imemoryowner-1) `interface` implementation, as well as the `Memory<T>` property. The syntax is virtually identical to the syntax used with `MemoryOwner<T>`, except for the differences mentioned earlier.

For example, suppose you have a method where you need to allocate a temporary buffer of a specified size (let's call this value `length`), and then use it to perform some work. A first, inefficient version might look like this:

```csharp
byte[] buffer = new byte[length];

// Use buffer here
```

This version isn't ideal because it allocates a new buffer every time you use this code, and then throws it away immediately. This approach puts more pressure on the garbage collector. You can optimize the preceding code by using [`ArrayPool<T>`](/dotnet/api/system.buffers.arraypool-1):

```csharp
// Using directive to access the ArrayPool<T> type
using System.Buffers;

int[] buffer = ArrayPool<int>.Shared.Rent(length);

try
{
    // Slice the span, as it might be larger than the requested size
    Span<int> span = buffer.AsSpan(0, length);

    // Use the span here
}
finally
{
    ArrayPool<int>.Shared.Return(buffer);
}
```

The preceding code rents a buffer from an array pool, but it's more verbose and error-prone. You need to be careful with the `try/finally` block to make sure you always return the rented buffer to the pool. You can rewrite it by using the `SpanOwner<T>` type, like so:

```csharp
// Be sure to include this using at the top of the file:
using Microsoft.Toolkit.HighPerformance.Buffers;

using SpanOwner<int> buffer = SpanOwner<int>.Allocate(length);

Span<int> span = buffer.Span;

// Use the span here, no slicing necessary
```

The `SpanOwner<T>` instance internally rents an array, and takes care of returning it to the pool when it goes out of scope. You no longer need to use a `try/finally` block either, as the C# compiler adds that automatically when expanding that `using` statement. As such, you can see the `SpanOwner<T>` type as a lightweight wrapper around the `ArrayPool<T>` APIs. It makes them both more compact and easier to use, reducing the amount of code that you need to write to properly rent and dispose short lived buffers. You can see how using `SpanOwner<T>` makes the code much shorter and more straightforward.

> [!NOTE]
> As this is a stack-only type, it relies on the duck-typed `IDisposable` pattern introduced with C# 8. That pattern is shown in the preceding sample: the `SpanOwner<T>` type is used within a `using` block despite the fact that the type doesn't implement the `IDisposable` interface at all, and it's also never boxed. The functionality is just the same: as soon as the buffer goes out of scope, it is automatically disposed. The APIs in `SpanOwner<T>` rely on this pattern for extra performance: they assume that the underlying buffer is never disposed as long as the `SpanOwner<T>` type is in scope. They don't perform the additional checks that are done in `MemoryOwner<T>` to ensure that the buffer is still available before returning a `Memory<T>` or `Span<T>` instance from it. As such, always use this type with a `using` block or expression. Not doing so causes the underlying buffer not to be returned to the shared pool. Technically, you can achieve the same result by manually calling `Dispose` on the `SpanOwner<T>` type (which doesn't require C# 8), but that approach is error prone and hence not recommended.

## Examples

You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.HighPerformance.UnitTests).
