---
title: .NET MAUI Community Toolkit - Markup
author: bijington
description: C# Markup is a set of fluent helper methods and classes designed to simplify the process of building declarative .NET Multi-platform App UI (.NET MAUI) user interfaces in code.
ms.date: 02/13/2022
---

# C# Markup

C# Markup is a set of fluent helper methods and classes designed to simplify the process of building declarative .NET Multi-platform App UI (.NET MAUI) user interfaces in code. The fluent API provided by C# Markup is available in the `CommunityToolkit.Maui.Markup` namespace.

[!INCLUDE [docs under construction](../includes/preview-note.md)]

Just as with XAML, C# Markup enables a clean separation between UI markup and UI logic. This can be achieved by separating UI markup and UI logic into distinct partial class files. For example, for a login page the UI markup would be in a file named `LoginPage.cs`, while the UI logic would be in a file named `LoginPage.logic.cs`.

C# Markup is available on all platforms supported by .NET MAUI.

## NuGet package

The C# Markup package can be included in your project(s) as decribed in our [Getting started](../get-started.md#communitytoolkitmauimarkup) guide.

## Example

The following example shows setting the page content to a new [`Grid`](xref:Microsoft.Maui.Controls.Grid) containing a [`Label`](xref:Microsoft.Maui.Controls.Label) and an [`Entry`](xref:Microsoft.Maui.Controls.Entry), in C#:

```csharp
Grid grid = new Grid();

Label label = new Label { Text = "Code: " };
grid.Children.Add(label);
GridLayout.SetColumn(label, 0);
GridLayout.SetRow(label, 0);

Entry entry = new Entry
{
    Placeholder = "Enter number",
    Keyboard = Keyboard.Numeric,
    BackgroundColor = Colors.AliceBlue,
    TextColor = Colors.Black,
    FontSize = 15,
    HeightRequest = 44,
    Margin = new Thickness(5)
};
grid.Children.Add(entry);
GridLayout.SetColumn(label, 1);
GridLayout.SetRow(label, 0);
entry.SetBinding(Entry.TextProperty, new Binding(nameof(ViewModel.RegistrationCode));

Content = grid;
```

This example creates a [`Grid`](xref:Microsoft.Maui.Controls.Grid) object, with child [`Label`](xref:Microsoft.Maui.Controls.Label) and [`Entry`](xref:Microsoft.Maui.Controls.Entry) objects. The `Label` displays text, and the `Entry` data binds to the `RegistrationCode` property of the viewmodel. Each child view is set to appear in a specific row in the `Grid`, and the `Entry` spans all the columns in the `Grid`. In addition, the height of the `Entry` is set, along with its keyboard, colors, the font size of its text, and its `Margin`. Finally, the `Page.Content` property is set to the `Grid` object.

C# Markup enables this code to be re-written using its fluent API:

```csharp
Content = new Grid
{
    Children =
    {
        new Label { Text = "Code:" }
            .Column(0)
            .Row(0),

        new Entry
            {
                Placeholder = "Enter number",
                Keyboard = Keyboard.Numeric,
                BackgroundColor = Colors.AliceBlue,
                TextColor = Colors.Black
            }
            .FontSize(15)
            .Height(44)
            .Margin(5, 5)
            .Column(1)
            .Row(0)
            .Bind(Entry.TextProperty, nameof(ViewModel.RegistrationCode))
    }
};
```

This example is identical to the previous example, but the C# Markup fluent API simplifies the process of building the UI in C#.


> [!NOTE]
> C# Markup includes extension methods that set specific view properties. These extension methods are not meant to replace all property setters. Instead, they are designed to improve code readability, and can be used in combination with property setters. It's recommended to always use an extension method when one exists for a property, but you can choose your preferred balance.