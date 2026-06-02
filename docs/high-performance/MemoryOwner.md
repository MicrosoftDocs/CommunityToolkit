---
title: MemoryOwner\<T>
author: Sergio0694
description: A buffer type implementing `IMemoryOwner<T>` that rents memory from a shared pool
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, parallel, high performance, net core, net standard
dev_langs:
  - csharp
---

# MemoryOwner\<T> class

The [`MemoryOwner<T>`](/dotnet/api/microsoft.toolkit.highperformance.buffers.memoryowner-1) class is a buffer type that implements [`IMemoryOwner<T>`](/dotnet/api/system.buffers.imemoryowner-1). It includes an embedded length property and a series of performance-oriented APIs. It's essentially a lightweight wrapper around the [`ArrayPool<T>`](/dotnet/api/system.buffers.arraypool-1) type, with some additional helper utilities.

> **Platform APIs:** [`MemoryOwner<T>`](/dotnet/api/microsoft.toolkit.highperformance.buffers.memoryowner-1), [`AllocationMode`](/dotnet/api/microsoft.toolkit.highperformance.buffers.allocationmode)

## How it works

`MemoryOwner<T>` has the following main features:

- One of the main issues with arrays returned by the `ArrayPool<T>` APIs and with `IMemoryOwner<T>` instances returned by the [`MemoryPool<T>`](/dotnet/api/system.buffers.memorypool-1) APIs is that the size you specify is used only as a _minimum_ size: the actual size of the returned buffers might be greater. `MemoryOwner<T>` solves this problem by also storing the original requested size, so [`Memory<T>`](/dotnet/api/system.memory-1) and [`Span<T>`](/dotnet/api/system.span-1) instances retrieved from it never need to be manually sliced.
- When you use `IMemoryOwner<T>`, getting a `Span<T>` for the underlying buffer requires first getting a `Memory<T>` instance, and then a `Span<T>`. This process is fairly expensive and often unnecessary, as you might not need the intermediate `Memory<T>`. Instead, `MemoryOwner<T>` has an additional `Span` property that's extremely lightweight because it directly wraps the internal `T[]` array rented from the pool.
- The pool doesn't clear buffers it rents by default. If the pool didn't clear the buffers when it previously returned them, they might contain garbage data. Normally, you need to clear these rented buffers manually, which can be verbose, especially when done frequently. `MemoryOwner<T>` offers a more flexible approach through the `Allocate(int, AllocationMode)` API. This method not only allocates a new instance of exactly the requested size but also lets you specify which allocation mode to use: either the same one as `ArrayPool<T>`, or one that automatically clears the rented buffer.
- Sometimes you might rent a buffer with a greater size than what you actually need, and then resize it. Normally, you'd need to rent a new buffer and copy the region of interest from the old buffer. Instead, `MemoryOwner<T>` exposes a `Slice(int, int)` API that returns a new instance wrapping the specified area of interest. This approach skips renting a new buffer and copying the items entirely.

## Syntax

Here's an example of how to rent a buffer and retrieve a `Memory<T>` instance:

```csharp
// Be sure to include this using at the top of the file:
using Microsoft.Toolkit.HighPerformance.Buffers;

using (MemoryOwner<int> buffer = MemoryOwner<int>.Allocate(42))
{
    // Both memory and span have exactly 42 items.
    Memory<int> memory = buffer.Memory;
    Span<int> span = buffer.Span;

    // Writing to the span modifies the underlying buffer.
    span[0] = 42;
}
```

In this example, you use a `using` block to declare the `MemoryOwner<T>` buffer. This approach is particularly useful because the underlying array is automatically returned to the pool at the end of the block. If you don't have direct control over the lifetime of a `MemoryOwner<T>` instance, the buffer is returned to the pool when the garbage collector finalizes the object. In both cases, the rented buffers are always correctly returned to the shared pool.

## When should you use this type?

You can use `MemoryOwner<T>` as a general-purpose buffer type. It minimizes the number of allocations over time because it internally reuses the same arrays from a shared pool. A common use case is to replace `new T[]` array allocations, especially when you do repeated operations that either require a temporary buffer to work on or produce a buffer as a result.

Suppose you have a dataset consisting of a series of binary files, and you need to read all these files and process them in some way. To properly separate your code, you might write a method that simply reads one binary file, which might look like this:

```csharp
public static byte[] GetBytesFromFile(string path)
{
    using Stream stream = File.OpenRead(path);

    byte[] buffer = new byte[(int)stream.Length];

    stream.Read(buffer, 0, buffer.Length);

    return buffer;
}
```

Note the `new byte[]` expression. If you read a large number of files, you allocate many new arrays, which puts a lot of pressure on the garbage collector. You might want to refactor this code by using buffers rented from a pool, like so:

```csharp
public static (byte[] Buffer, int Length) GetBytesFromFile(string path)
{
    using Stream stream = File.OpenRead(path);

    byte[] buffer = ArrayPool<T>.Shared.Rent((int)stream.Length);

    stream.Read(buffer, 0, (int)stream.Length);

    return (buffer, (int)stream.Length);
}
```

By using this approach, you rent buffers from a pool, which means that in most cases you skip an allocation. Additionally, since rented buffers aren't cleared by default, you can also save the time needed to fill them with zeros, which gives you another small performance improvement. In the preceding example, loading 1,000 files brings the total allocation size from around 1 MB down to just 1,024 bytes. You effectively allocate and reuse just a single buffer.

The preceding code has two main problems:

- `ArrayPool<T>` might return buffers that have a size greater than the requested size. To work around this problem, you need to return a tuple that also indicates the actual used size in your rented buffer.
- By simply returning an array, you need to be extra careful to properly track its lifetime and to return it to the appropriate pool. You might work around this problem by using `MemoryPool<T>` instead and by returning an `IMemoryOwner<T>` instance, but you still have the problem of rented buffers having a greater size than what you need. Additionally, `IMemoryOwner<T>` has some overhead when retrieving a `Span<T>` to work on, due to it being an interface, and the fact that you always need to get a `Memory<T>` instance first, and then a `Span<T>`.

To solve both these problems, you can refactor this code again by using `MemoryOwner<T>`:

```csharp
public static MemoryOwner<byte> GetBytesFromFile(string path)
{
    using Stream stream = File.OpenRead(path);

    MemoryOwner<byte> buffer = MemoryOwner<byte>.Allocate((int)stream.Length);

    stream.Read(buffer.Span);

    return buffer;
}
```

The returned `IMemoryOwner<byte>` instance disposes the underlying buffer and returns it to the pool when its [`IDisposable.Dispose`](/dotnet/api/system.idisposable.dispose) method is invoked. You can use it to get a `Memory<T>` or `Span<T>` instance to interact with the loaded data, and then dispose the instance when you no longer need it. Additionally, all the `MemoryOwner<T>` properties (like `MemoryOwner<T>.Span`) respect the initial requested size you used, so you no longer need to manually keep track of the effective size within the rented buffer.

## Examples

You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.HighPerformance.UnitTests).
