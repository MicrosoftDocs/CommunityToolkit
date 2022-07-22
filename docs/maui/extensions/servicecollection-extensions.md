---
title: ServiceCollectionExtensions - .NET MAUI Community Toolkit
author: rjygraham
description: "The ServiceCollectionExtensions provide a series of extension methods that simplify registering Views and ViewModels within a .NET MAUI  IServiceCollection."
ms.date: 07/19/2022
---

<!-- markdownlint-configure-file { "MD024": { "allow_different_nesting": true } } -->

# ServiceCollectionExtensions

The `ServiceCollectionExtensions` provide a series of extension methods that simplify registering Views and their associated ViewModels within the .NET MAUI `IServiceCollection`.

The `ServiceCollectionExtensions` can be found under the `CommunityToolkit.Maui` namespace so just add the following line to get started:

```csharp
using CommunityToolkit.Maui;
```

> NOTE: These extension methods only register the View and ViewModels in the `IServiceCollection`. Developers are still responsible for assigning the injected instance of the ViewModel to the `BindingContext` property of the View.
>
> Additionally, these extension methods assume there is a one-to-one relationship between View and ViewModel and that both share the same lifetime. Developers will need to revert to registering Views and ViewModels individually in order to specify differing lifetimes or to handle scenarios in which multiple Views  use the same ViewModel.

## Register Views and ViewModels

The following methods allow you to register Views and ViewModels within the .NET MAUI `IServiceCollection`.

### AddScoped<TView, TViewModel>(IServiceCollection)

Adds a scoped View of the type specified in TView and ViewModel of the type TViewModel to the specified IServiceCollection.

```csharp
using CommunityToolkit.Maui;

namespace CommunityToolkit.Maui.Sample;

public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        var builder = MauiApp.CreateBuilder()
                            .UseMauiCommunityToolkit()
                            .UseMauiApp<App>();

        builder.Services.AddScoped<HomePage, HomePageViewModel>();
    }
}
```

#### Type Parameters

##### TView

The type of the View to add. Constrained to `BindableObject`

##### TViewModel

The type of the ViewModel to add. Constrained to reference types implementing `INotifyPropertyChanged`

#### Parameters

##### `services` [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)

The [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection) to add the View and ViewModel to.

#### Returns

[IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)
A reference to this instance after the operation has completed.

### AddSingleton<TView, TViewModel>(IServiceCollection)

Adds a singleton View of the type specified in TView and ViewModel of the type TViewModel to the specified IServiceCollection.

```csharp
using CommunityToolkit.Maui;

namespace CommunityToolkit.Maui.Sample;

public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        var builder = MauiApp.CreateBuilder()
                            .UseMauiCommunityToolkit()
                            .UseMauiApp<App>();

        builder.Services.AddSingleton<HomePage, HomePageViewModel>();
    }
}
```

#### Type Parameters

##### TView

The type of the View to add. Constrained to `BindableObject`

##### TViewModel

The type of the ViewModel to add. Constrained to reference types implementing `INotifyPropertyChanged`

#### Parameters

##### `services` [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)

The [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection) to add the View and ViewModel to.

#### Returns

[IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)
A reference to this instance after the operation has completed.

### AddTransient<TView, TViewModel>(IServiceCollection)

Adds a transient View of the type specified in TView and ViewModel of the type TViewModel to the specified IServiceCollection.

```csharp
using CommunityToolkit.Maui;

namespace CommunityToolkit.Maui.Sample;

public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        var builder = MauiApp.CreateBuilder()
                            .UseMauiCommunityToolkit()
                            .UseMauiApp<App>();

        builder.Services.AddTransient<HomePage, HomePageViewModel>();
    }
}
```

#### Type Parameters

##### TView

The type of the View to add. Constrained to `BindableObject`

##### TViewModel

The type of the ViewModel to add. Constrained to reference types implementing `INotifyPropertyChanged`

#### Parameters

##### `services` [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)

The [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection) to add the View and ViewModel to.

#### Returns

[IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)
A reference to this instance after the operation has completed.

## Register Views and ViewModels With Shell Route

The following methods allow you to register Views and ViewModels within the .NET MAUI `IServiceCollection` and explicitly register a route to the View within .NET MAUI Shell routing.

### AddScopedWithShellRoute<TView, TViewModel>(services, route, factory)

Adds a scoped View of the type specified in TView and ViewModel of the type TViewModel to the specified IServiceCollection and registers the view for Shell navigation at the route specified in the route parameter. An optional `RouteFactory` can be provided to control View construction.

```csharp
using CommunityToolkit.Maui;

namespace CommunityToolkit.Maui.Sample;

public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        var builder = MauiApp.CreateBuilder()
                            .UseMauiCommunityToolkit()
                            .UseMauiApp<App>();

        builder.Services.AddScopedWithShellRoute<HomePage, HomePageViewModel>("HomePage");
    }
}
```

#### Type Parameters

##### TView

The type of the View to add. Constrained to `NavigableElement`

##### TViewModel

The type of the ViewModel to add. Constrained to reference types implementing `INotifyPropertyChanged`

#### Parameters

##### `services` [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)

The [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection) to add the View and ViewModel to.

##### `route` [string](/dotnet/api/system.string)

The route to which the View can be navigated within .NET MAUI Shell.

##### `factory (optional)` `RouteFactory`

The `RouteFactory` to control View construction.

#### Returns

[IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)
A reference to this instance after the operation has completed.

### AddSingletonWithShellRoute<TView, TViewModel>(services, route, factory)

Adds a singleton View of the type specified in TView and ViewModel of the type TViewModel to the specified IServiceCollection and registers the view for Shell navigation at the route specified in the route parameter. An optional `RouteFactory` can be provided to control View construction.

```csharp
using CommunityToolkit.Maui;

namespace CommunityToolkit.Maui.Sample;

public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        var builder = MauiApp.CreateBuilder()
                            .UseMauiCommunityToolkit()
                            .UseMauiApp<App>();

        builder.Services.AddSingletonWithShellRoute<HomePage, HomePageViewModel>("HomePage");
    }
}
```

#### Type Parameters

##### TView

The type of the View to add. Constrained to `NavigableElement`

##### TViewModel

The type of the ViewModel to add. Constrained to reference types implementing `INotifyPropertyChanged`

#### Parameters

##### `services` [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)

The [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection) to add the View and ViewModel to.

##### `route` [string](/dotnet/api/system.string)

The route to which the View can be navigated within .NET MAUI Shell.

##### `factory (optional)` `RouteFactory`

The `RouteFactory` to control View construction.

#### Returns

[IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)
A reference to this instance after the operation has completed.

### AddTransientWithShellRoute<TView, TViewModel>(services, route, factory)

Adds a transient View of the type specified in TView and ViewModel of the type TViewModel to the specified IServiceCollection and registers the view for Shell navigation at the route specified in the route parameter. An optional `RouteFactory` can be provided to control View construction.

```csharp
using CommunityToolkit.Maui;

namespace CommunityToolkit.Maui.Sample;

public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        var builder = MauiApp.CreateBuilder()
                            .UseMauiCommunityToolkit()
                            .UseMauiApp<App>();

        builder.Services.AddTransientWithShellRoute<HomePage, HomePageViewModel>("HomePage");
    }
}
```

#### Type Parameters

##### TView

The type of the View to add. Constrained to `NavigableElement`

##### TViewModel

The type of the ViewModel to add. Constrained to reference types implementing `INotifyPropertyChanged`

#### Parameters

##### `services` [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)

The [IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection) to add the View and ViewModel to.

##### `route` [string](/dotnet/api/system.string)

The route to which the View can be navigated within .NET MAUI Shell.

##### `factory (optional)` `RouteFactory`

The `RouteFactory` to control View construction.

#### Returns

[IServiceCollection](/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection)
A reference to this instance after the operation has completed.

## API

You can find the source code for `ServiceCollectionExtensions` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Extensions/ServiceCollectionExtensions.shared.cs).
