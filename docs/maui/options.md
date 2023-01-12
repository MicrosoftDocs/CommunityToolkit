---
title: Options - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: CommunityToolkit.Maui.Options allows to customize the CommunityToolkit.Maui.
ms.date: 09/14/2022
---

# CommunityToolkit.Maui.Options

`CommunityToolkit.Maui.Options` allows developers to customize `CommunityToolkit.Maui`. The toolkit may behave different depends on these settings.

`Options` should be assigned at startup when calling `.UseMauiCommunityToolkit()`:

```cs
var builder = MauiApp.CreateBuilder();
builder.UseMauiCommunityToolkit(options =>
{
    options.SetShouldSuppressExceptionsInConverters(false);
    options.SetShouldSuppressExceptionsInBehaviors(false);
    options.SetShouldSuppressExceptionsInAnimations(false);
})
```

## SetShouldSuppressExceptionsInConverters

When set to `true`, if a converter implementing `CommunityToolkit.Maui.Converters.BaseConverter` throws an `Exception`, the `Exception` will be caught, logged via `Debug.WriteLine()`, and a predetermined default value will be returned.

Default value is `false`.

### Example
This option is enabled when calling `.UseMauiCommunityToolkit()`:

```csharp
var builder = MauiApp.CreateBuilder();
builder.UseMauiCommunityToolkit(options =>
{
    options.SetShouldSuppressExceptionsInConverters(true);
})
```

### Default Return Values
When set to `true`, a default value will be returned when a `Converter` throws an `Exception`.

Two default values are included:

- `public object? ICommunityToolkitValueConverter.DefaultConvertReturnValue { get; set; }`
   - `Default value returned when Convert(object? value, Type targetType, object? parameter, CultureInfo? culture)` throws an `Exception`
- `public object ICommunityToolkitValueConverter.DefaultConvertBackReturnValue { get; set; }`
   - `Default value returned when ConvertBack(object? value, Type targetType, object? parameter, CultureInfo? culture)` throws an `Exception`

Here is an example setting the default values for `BoolToObjectConverter`:

XAML
```xml
<ContentPage.Resources>
    <SolidColorBrush x:Key="TrueColorBrush">Green</SolidColorBrush>
    <SolidColorBrush x:Key="FalseColorBrush">Red</SolidColorBrush>
    <toolkit:BoolToObjectConverter x:Key="BoolToColorBrushConverter" 
                                TrueObject="{StaticResource TrueColorBrush}" 
                                FalseObject="{StaticResource FalseColorBrush}"
                                DefaultConvertReturnValue="{StaticResource FalseColorBrush}"
                                DefaultConvertBackReturnValue="False"/>
</ContentPage.Resources>
```

C#
```csharp
var boolToColorBrushConverter = new BoolToObjectConverter
{
    TrueObject = new SolidColorBrush(Colors.Green),
    FalseObject = new SolidColorBrush(Colors.Red),
    DefaultConvertReturnValue = new SolidColorBrush(Colors.Red),
    DefaultConvertBackReturnValue = false
};
```

## SetShouldSuppressExceptionsInAnimations
When set to `true`, if an `Animation` implementing `CommunityToolkit.Maui.Behaviors.AnimationBehavior` throws an `Exception`, the `Exception` will be caught and will be logged via `Debug.WriteLine()`.

Default value is `false`.

### Example
This option is enabled when calling `.UseMauiCommunityToolkit()`:

```csharp
var builder = MauiApp.CreateBuilder();
builder.UseMauiCommunityToolkit(options =>
{
    options.SetShouldSuppressExceptionsInAnimations(true);
})
```

## SetShouldSuppressExceptionsInBehaviors

When set to `true`, if a `Behavior` implementing `CommunityToolkit.Maui.Behaviors.BaseBehavior` throws an `Exception`, the `Exception` will be caught and will be logged via `Debug.WriteLine()`.

Default value is `false`.

### Example
This option is enabled when calling `.UseMauiCommunityToolkit()`:

```csharp
var builder = MauiApp.CreateBuilder();
builder.UseMauiCommunityToolkit(options =>
{
    options.SetShouldSuppressExceptionsInBehaviors(true);
})
```