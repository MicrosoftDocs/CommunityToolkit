---
title: StringPool
author: Sergio0694
description: A type implementing a configurable pool for string instances
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, parallel, high performance, net core, net standard
dev_langs:
  - csharp
---

# StringPool class

The [StringPool](/dotnet/api/microsoft.toolkit.highperformance.buffers.stringpool) type implements a configurable pool for `string` instances. Use this pool to minimize allocations when you create multiple `string` instances from buffers of `char` or `byte` values. It provides a mechanism that's somewhat similar to [`string` interning](/dotnet/api/system.string.intern). The main differences are that the pool is configurable, you can reset it, it uses a best-effort policy, and it doesn't require preinstantiating `string` objects. So, it can save the initial allocations when working on temporary buffers.

> **Platform APIs:** [StringPool](/dotnet/api/microsoft.toolkit.highperformance.buffers.stringpool)

## Syntax

The main entry point for `StringPool` is its `GetOrAdd(ReadOnlySpan<char>)` API. This API returns a `string` instance that matches the contents of the input [`ReadOnlySpan<char>`](/dotnet/api/system.readonlyspan-1). The API might get the returned object from the internal pool.

For example, imagine you have an input `string` that represents the URL of a given web request, and you want to retrieve a `string` with just the host name. If you get a large number of requests, possibly for a small number of hosts, you might want to cache those `string` instances. You can do so by using the `StringPool` type as follows:

```csharp
public static string GetHost(string url)
{
    // We assume the input might start either with eg. https:// (or other prefix),
    // or directly with the host name. Furthermore, we also assume that the input
    // URL will always have a '/' character right after the host name.
    // For instance: "https://learn.microsoft.com/dotnet/api/system.string.intern".
    int
        prefixOffset = url.AsSpan().IndexOf(stackalloc char[] { ':', '/', '/' }),
        startIndex = prefixOffset == -1 ? 0 : prefixOffset + 3,
        endIndex = url.AsSpan(startIndex).IndexOf('/');

    // In this example, it would be "learn.microsoft.com"
    ReadOnlySpan<char> span = url.AsSpan(startIndex, endIndex);

    return StringPool.Shared.GetOrAdd(span);
}
```

The preceding method doesn't allocate at all if the requested `string` is already present in the cache. The lookup uses just a `ReadOnlySpan<char>` as input, which represents a view on the input URL `string`.

The `StringPool` type can also be useful when you parse raw requests by using a different encoding, such as UTF8. There's a `GetOrAdd` overload that takes an input `ReadOnlySpan<byte>` and an [`Encoding`](/dotnet/api/system.text.encoding) instance. This overload uses a temporary buffer rented from the pool to retrieve a `ReadOnlySpan<char>` value to use for the lookup. This approach can greatly reduce the number of allocations depending on your specific use case scenario.

## Examples

You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.HighPerformance.UnitTests).
