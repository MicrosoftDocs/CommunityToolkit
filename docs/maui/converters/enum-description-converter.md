---
title: EnumDescriptionConverter - .NET MAUI Community Toolkit
author: BillyMartin1964
description: "Converts an Enum value to its display string using DisplayAttribute or DescriptionAttribute."
ms.date: 06/10/2024
---

# EnumDescriptionConverter


The `EnumDescriptionConverter` is a one way converter that returns a `string` representing the display name or description of an `Enum` value. It uses the [`DisplayAttribute`](https://learn.microsoft.com/dotnet/api/system.componentmodel.dataannotations.displayattribute) or [`DescriptionAttribute`](https://learn.microsoft.com/dotnet/api/system.componentmodel.descriptionattribute) if present, otherwise returns the enum name.
The `EnumDescriptionConverter` is a one way converter that returns a `string` representing the display name or description of an `Enum` value. It uses the [`DisplayAttribute`](/dotnet/api/system.componentmodel.dataannotations.displayattribute) or [`DescriptionAttribute`](/dotnet/api/system.componentmodel.descriptionattribute) if present, otherwise returns the enum name.

The `Convert` method returns the value of the `DisplayAttribute.Name` if defined, otherwise the value of the `DescriptionAttribute.Description` if defined, otherwise the enum name as a string.

The `ConvertBack` method is not supported.

[!INCLUDE [common converter properties](../includes/communitytoolkit-converter.md)]

## Syntax

### XAML

#### Including the XAML namespace

[!INCLUDE [XAML usage guidance](../includes/xaml-usage.md)]

#### Using the EnumDescriptionConverter

The `EnumDescriptionConverter` can be used as follows in XAML:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="CommunityToolkit.Maui.Sample.Pages.Converters.EnumDescriptionConverterPage">

    <ContentPage.Resources>
        <ResourceDictionary>
            <toolkit:EnumDescriptionConverter x:Key="EnumDescriptionConverter" />
        </ResourceDictionary>
    </ContentPage.Resources>

    <Label Text="{Binding MyEnumValue, Converter={StaticResource EnumDescriptionConverter}}" />
</ContentPage>
```

### C#

The `EnumDescriptionConverter` can be used as follows in C#:

```csharp
class EnumDescriptionConverterPage : ContentPage
{
    public EnumDescriptionConverterPage()
    {
        var label = new Label();
        label.SetBinding(
            Label.TextProperty,
            new Binding(
                static (ViewModel vm) => vm.MyEnumValue,
                converter: new EnumDescriptionConverter()));
        Content = label;
    }
}
```

### C# Markup

Our [`CommunityToolkit.Maui.Markup`](../markup/markup.md) package provides a concise way to use this converter in C#.

```csharp
using CommunityToolkit.Maui.Markup;

class EnumDescriptionConverterPage : ContentPage
{
    public EnumDescriptionConverterPage()
    {
        Content = new Label()
            .Bind(
                Label.TextProperty,
                static (ViewModel vm) => vm.MyEnumValue,
                converter: new EnumDescriptionConverter());
    }
}
```

## Examples


Suppose you have an enum defined as follows:

```csharp
public enum Status
{
    [Display(Name = "Active User")]
    Active,
    [Description("Inactive User")]
    Inactive,
    Pending
}
```

Binding a value of `Status.Active` to the converter will display "Active User". If the value is `Status.Inactive`, it will display "Inactive User". If the value is `Status.Pending`, it will display "Pending" (the enum name).

### Localized Enum Example

You can use `DisplayAttribute` with `ResourceType` to provide localized display names:

```csharp
public enum Status
{
    [Display(Name = "Active_User", ResourceType = typeof(Resources.StatusResources))]
    Active,
    [Display(Name = "Inactive_User", ResourceType = typeof(Resources.StatusResources))]
    Inactive,
    Pending
}
```

Where `StatusResources` is a resource file containing:

| Key           | Value (en-US)   | Value (fr-FR)   |
|---------------|-----------------|-----------------|
| Active_User   | Active User     | Utilisateur Actif|
| Inactive_User | Inactive User   | Utilisateur Inactif|

> **Note:** If the resource key is missing or not found, the converter will return the enum member name (e.g., `Active`). This ensures a string is always returned, but may not be localized or user-friendly.


## API

You can find the source code for `EnumDescriptionConverter` over on the [CommunityToolkit.Maui GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Converters/EnumDescriptionConverter.shared.cs).

- If `DisplayAttribute.Name` is defined, it is used.
- If `DescriptionAttribute.Description` is defined, it is used.
- Otherwise, the enum name is returned.

**Namespace:** `CommunityToolkit.Maui.Converters`

**Class:** `EnumDescriptionConverter`

**Base:** `BaseConverterOneWay<Enum, string>`

## See Also
- [DisplayAttribute Documentation](/dotnet/api/system.componentmodel.dataannotations.displayattribute)
- [DescriptionAttribute Documentation](/dotnet/api/system.componentmodel.descriptionattribute)
