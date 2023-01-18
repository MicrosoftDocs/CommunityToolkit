---
title: Style extensions - .NET MAUI Community Toolkit
author: brminnick
description: Style<T> provides a series of fluent extension methods that support configuring Microsoft.Maui.Controls.Style
ms.date: 03/28/2022
---

# Style\<T\>

`Style<T>` provides a series of fluent extension methods that support configuring `Microsoft.Maui.Controls.Style`.

## Constructors

`Style<T>` provides the following constructors:

```csharp
public Style(BindableProperty property, object value);
public Style(params (BindableProperty Property, object Value)[] setters);
```

These constructors can be used to initialize `Style<T>` and assign it to a `Microsoft.Maui.Controls.Style` for a single setter, like so:

```csharp
new Label
{
    Style = new Style<Entry>(Entry.TextColorProperty, Colors.Red)
}
```

These constructors can also be used to initialize `Style<T>` and assign it to a `Microsoft.Maui.Controls.Style` for multiple setter using types, like so:

```csharp
new Label
{
    Style = new Style<Entry>(
            (Entry.TextColorProperty, Colors.Red),
            (Entry.BackgroundColorProperty, Colors.White),
            (Entry.FontAttributesProperty, FontAttributes.Bold))
}
```

## Properties

`Style<T>` contains one property, `MauiStyle`.

This property leverages `Microsoft.Maui.Controls.Style` and is assigned upon initialization.

The styles added to, and implemented in, `Style<T>` are stored in the `MauiStyle` property.

```cs
public Microsoft.Maui.Controls.Style MauiStyle { get; }
```

## Methods

`Style<T>` offers a fluent extension methods to `Add` additional styles, to set `ApplyToDerivedTypes`, to set `BasedOn`, and to set `CanCascade`.

### Add

`Style<T>` offers multiple ways to add to an existing style:

```csharp
public Style<T> Add(BindableProperty property, object value);
public Style<T> AddAppThemeBinding(BindableProperty property, object light, object dark);
public Style<T> Add(params (BindableProperty Property, object Value)[] setters);
public Style<T> AddAppThemeBindings(params (BindableProperty Property, object Light, object Dark)[] setters);
public Style<T> Add(params Behavior[] behaviors);
public Style<T> Add(params TriggerBase[] triggers);
```

The `Add` methods can be used like so:

```csharp
new Label
{
    Style = new Style<Label>()
                .AddAppThemeBinding(Label.TextColorProperty, Colors.Red, Colors.Orange)
                .Add((Label.BackgroundColorProperty, Colors.White), (Label.FontAttributesProperty, FontAttributes.Bold))
                .Add(new NumericValidationBehavior())
                .Add(new EventTrigger { Event = nameof(Label.Focused) });
}
```

For more information on the use of `AddAppThemeBinding` refer to the [Theming](../theming.md) documentation.

### ApplyToDerivedTypes

The fluent extension method, `ApplyToDerivedTypes(bool value)`, sets the value of the `AppleToDerivedTypes` property:

```cs
public Style<T> ApplyToDerivedTypes(bool value);
```

It can be used like so:

```csharp
new Label
{
    Style = new Style<Label>(Label.TextColorProperty, Colors.Red)
                .ApplyToDerivedTypes(true);
}
```

### BasedOn

The fluent extension method, `BasedOn(Style value)`, sets the value of the `BasedOn` property:

```cs
public Style<T> BasedOn(Style value);
```

It can be used like so to base the current style on an existing style:

```csharp
new VerticalStackLayout
{
    Children = 
    {
        new Label
        {
            Style = new Style<Label>(Label.TextColorProperty, Colors.Red)
        }.Assign(out Label redTextLabel),

        new Label
        {
          Style = new Style<Label>().BasedOn(redTextLabel.Style);
        }
    }
};
```

### CanCascade

The fluent extension method, `CanCascade(bool value)`, sets the value of the `CanCascade` property:

```cs
public Style<T> CanCascade(bool value);
```

It can be used like so:

```csharp
new Label
{
  Style = new Style<Label>(Label.TextColorProperty, Colors.Red).CanCascade(true);
}
```
