---
title: ThrowHelper class
author: Sergio0694
description: Helper methods to efficiently throw exceptions
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, debug, net core, net standard
dev_langs:
  - csharp
---

# ThrowHelper class

The [ThrowHelper class](/dotnet/api/microsoft.toolkit.diagnostics.ThrowHelper) is a helper type that can be used to efficiently throw exceptions. It's meant to support the [Guard](Guard.md) APIs, and it should primarily be used in situations where developers need fine-grained control over the exception types being thrown, or over the exact exception message to include.

> **Platform APIs:** [`ThrowHelper`](/dotnet/api/microsoft.toolkit.diagnostics.ThrowHelper), [`Guard`](/dotnet/api/microsoft.toolkit.diagnostics.guard)

## Syntax

The `ThrowHelper` class exposes a series of `ThrowException` APIs that offer a 1:1 mapping to the constructors of all the available exception types. These methods are meant to be used in place of the classic `throw new Exception(...)` statement in code, to create smaller and more efficient code. Put simply:

```csharp
// Replace this...
throw new InvalidOperationException("Some custom message from my library");

// ...with this
ThrowHelper.ThrowInvalidOperationException("Some custom message from my library");
```

> [!NOTE]
> This change also results in a slightly different stack trace, as the exception is thrown by this helper method instead of directly by the original caller. The practical result is still the same as throwing an exception directly.

The `Guard` APIs provide an easy-to-use abstraction over many common checks that might need to be performed, so it's recommended to first try to see if there is a `Guard` API that can be used, and only fall back on using `ThrowHelper` if that's not the case. As mentioned before, this might be if your library needs to throw a specific exception type not present in the `Guard` APIs, or if you need full control on the exact arguments being included in the exception being thrown.

There are also generic overloads for all the available APIs, which can be used within expressions that require a return type of a specific type (for example, a switch expression). These overloads never return any value, but the return type is declared to allow the C# compiler to accept the usage of these APIs within expressions that wouldn't work with a method returning `void`. Consider the following example:

```csharp
int result = text switch
{
    "cat" => 0,
    "dog" => 1,
    _ => ThrowHelper.ThrowArgumentException<int>(nameof(text))
};
```

Here, `ThrowHelper` is used within an expression that requires a return type of type `int`, so you can use the generic overload of `ThrowArgumentException` to make this possible. The generic overload also works with patterns such as ternary operators (`x ? a : b`), null-coalescing operators (`x = a ?? b`), and null-coalescing assignment operators (`x ??= y`).

## Methods

There are lots of different methods and overloads in the `ThrowHelper` class. They provide access to the following exceptions (and map all their public constructors):

- [ArrayTypeMismatchException](/dotnet/api/system.ArrayTypeMismatchException)
- [ArgumentException](/dotnet/api/system.ArgumentException)
- [ArgumentNullException](/dotnet/api/system.ArgumentNullException)
- [ArgumentOutOfRangeException](/dotnet/api/system.ArgumentOutOfRangeException)
- [COMException](/dotnet/api/system.runtime.interopservices.COMException)
- [ExternalException](/dotnet/api/system.runtime.interopservices.ExternalException)
- [FormatException](/dotnet/api/system.FormatException)
- [InsufficientMemoryException](/dotnet/api/system.InsufficientMemoryException)
- [InvalidDataException](/dotnet/api/system.io.InvalidDataException)
- [InvalidOperationException](/dotnet/api/system.InvalidOperationException)
- [LockRecursionException](/dotnet/api/system.threading.LockRecursionException)
- [MissingFieldException](/dotnet/api/system.MissingFieldException)
- [MissingMemberException](/dotnet/api/system.MissingMemberException)
- [MissingMethodException](/dotnet/api/system.MissingMethodException)
- [NotSupportedException](/dotnet/api/system.NotSupportedException)
- [ObjectDisposedException](/dotnet/api/system.ObjectDisposedException)
- [OperationCanceledException](/dotnet/api/system.OperationCanceledException)
- [PlatformNotSupportedException](/dotnet/api/system.PlatformNotSupportedException)
- [SynchronizationLockException](/dotnet/api/system.threading.SynchronizationLockException)
- [TimeoutException](/dotnet/api/system.TimeoutException)
- [UnauthorizedAccessException](/dotnet/api/system.UnauthorizedAccessException)
- [Win32Exception](/dotnet/api/system.componentmodel.Win32Exception)

You can see the available constructors for each of these exception types from the linked docs. The respective `ThrowHelper` APIs offer a series of overloads corresponding to the existing constructors for that specified type. Each API is simply named "Throw" + the exception type.

## Technical details

The following section describes the impact of switching to `ThrowHelper` APIs over the standard `throw new Exception` statements with respect to the codegen. As mentioned previously, knowing these details isn't necessary to use these APIs, but for developers familiar with how the runtime works or with how the JIT processes code during execution, this section provides a clearer explanation of why using the `ThrowHelper` pattern results in more compact and faster code.

First, consider the code that the JIT compiler actually produces in these situations. This example uses the code generated on .NET Core 3.1 x64 as a reference, but the same concept applies to other runtimes and architectures as well.

Consider this simple type:

```csharp
public struct ExceptionTest
{
    private int number;

    public int GetValueIfNotZeroOrThrow()
    {
        if (number == 0)
        {
            throw new InvalidOperationException("The value must be != 0");
        }

        return number;
    }
}
```

This type is only meant to showcase the use of `ThrowHelper` APIs. It checks the value of the `number` field and throws if it's 0. Inspect the generated assembly code:

```x86asm
ExceptionTest.GetValueIfNotZeroOrThrow()
    mov eax, [rcx]              ; read number
    test eax, eax               ; if (number != 0)
    je short L0011              ; jump to faulting path (if == 0)
    ret                         ; return (number is already in eax)
    mov rcx, 0x7ff95cbaca80     ; exception setup...
    call 0x00007ff9bc6178f0
    mov rsi, rax
    mov ecx, 1
    mov rdx, 0x7ff96590c080
    call 0x00007ff9bc7403e0
    mov rdx, rax
    mov rcx, rsi
    call System.InvalidOperationException..ctor(System.String)
    mov rcx, rsi
    call 0x00007ff9bc5db3a0
    int3 ; finally throw the exception
```

You can see the code contains a lot of lines just dedicated to creating the exception being thrown. This can cause a large increase in the code size whenever you have many of these checks, because it reduces the efficiency of the instruction cache. In general, you want the size of your methods to be as small as possible.

The previous method, rewritten using the `ThrowHelper` APIs, looks like this:

```csharp
public int GetValueIfNotZeroOrThrow()
{
    if (number == 0)
    {
        ThrowHelper.ThrowInvalidOperationException("The value must be != 0");
    }

    return number;
}
```

Which results in the following assembly:

```x86asm
ExceptionTest.GetValueIfNotZeroOrThrow2()
    mov eax, [rcx]          ; load number
    test eax, eax           ; if (number != 0)
    je short L000f          ; faulting path (if == 0)
    ret                     ; return number (already in eax)
    mov rcx, 0x23435d85b98  ; load the exception message
    mov rcx, [rcx]
    call ThrowHelper.ThrowInvalidOperationException(System.String) ; ThrowHelper call!
    int3 ; return with fault
```

You can see that the resulting assembly is much smaller than before. The code to create the exception is moved out of the method, which also means you can reuse the same code from the `ThrowHelper` APIs, with different arguments, instead of inlining the exception throw in every method. Here there are only two `mov` instructions to load the `string` with the exception type, and then it jumps to the `ThrowHelper.ThrowInvalidOperationException` method. The JIT compiler is able to see that that method always throws, so it never inlines that call. And it makes sure to rewrite the conditional branches in the best way possible (specifically, knowing which branch is supposed to be executed, without faulting).

## Examples

You can find more examples in the [unit tests](https://github.com/CommunityToolkit/dotnet/tree/main/tests/CommunityToolkit.Diagnostics.UnitTests).
