---
title: DispatcherQueueExtensions
author: Sergio0694
description: Helpers for executing code on a specific UI thread through a DispatcherQueue instance.
keywords: dispatcher, dispatcherqueue, DispatcherHelper, DispatcherQueueExtensions
dev_langs:
  - csharp
category: Extensions
subcategory: Miscellaneous
discussion-id: 0
issue-id: 0
icon: Assets/Extensions.png
---

# DispatcherQueueExtensions

The `DispatcherQueueExtensions` type provides a collection of extensions methods for [`DispatcherQueue`](/uwp/api/windows.system.dispatcherqueue) objects that makes it easier to execute code on a specific UI thread. A `DispatcherQueue` instance can be retrieved and cached for later use, and then used through any of the available helper methods to dispatch a delegate invocation on it.

## Syntax

The `DispatcherQueueExtensions` type exposes a number of overloads of its `EnqueueAsync` method to dispatch either synchronous or asynchronous delegates, and to optionally have them return a value that is then relayed back to the caller through an awaitable task. Here are some examples of how these extension methods can be used:

```csharp
// Get a DispatcherQueue instance for later use. This has to be called on the UI thread,
// but it can then be cached for later use and accessed from a background thread as well.
DispatcherQueue dispatcherQueue = DispatcherQueue.GetForCurrentThread();

// Execute some code on the target dispatcher queue
await dispatcherQueue.EnqueueAsync(() =>
{
});

// Execute some code that also returns a value
int someValue = await dispatcherQueue.EnqueueAsync(() =>
{
    return 42;
});

// Execute some asynchronous code
await dispatcherQueue.EnqueueAsync(async () =>
{
    await Task.Delay(100);
});

// Execute some asynchronous code that also returns a value
int someOtherValue = await dispatcherQueue.EnqueueAsync(async () =>
{
    await Task.Delay(100);

    return 42;
});
```
