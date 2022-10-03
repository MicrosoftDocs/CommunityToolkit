---
title: Grid extensions - .NET MAUI Community Toolkit
author: brminnick
description: The Grid extensions provide a series of extension methods that support configuring a Grid.
ms.date: 05/17/2022
---

# Grid extensions

The `Grid` extensions provide a series of extension methods that support configuring a `Grid`.

## Defining Rows + Columns

To define rows and columns for a `Grid`, `CommunityToolkit.Maui.Markup` provides two helper methods:

- `Columns.Define`
- `Rows.Define`

To leverage these helper methods, we first add the following `using static` directive to the top of our class:

```cs
using static CommunityToolkit.Maui.Markup.GridRowsColumns;
```

After adding the above `using static` directive, we can then define our Row + Column sizes using the following values to set the `GridLength`:

| Microsoft.Maui.GridLength | XAML | CommunityToolkit.Maui.Markup.GridRowsColumns |
| --- | -- | -- |
| `GridLength.Auto` | `Auto` | `Auto` |
| `GridLength.Star` | `*` | `Star` |
| `new GridLength(2, GridLength.Star)` | `2*` | `Stars(2)` |
| `new GridLength(20, GridLength.Absolute)` | `20` | `20` |

Putting it all together, we can now define a Grid's Rows + Columns:

```cs
new Grid
{
    ColumnDefinitions = Columns.Define(30, Star, Stars(2)),
    RowDefinitions = Rows.Define(Auto, Star),   
};
```

### Example

The following example demonstrates how to create a `Grid` with 2 Rows:

- Row 0 Size: `GridLength.Auto`
- Row 1 Size:  `GridLength.Star` 

The following example demonstrates how to create a `Grid` with 3 Columns:

- Column 0 Size: `new GridLength(30, GridLength.Absolute)`
- Column 1 Size: `GridLength.Star`
- Column 2 Size: `new GridLength(GridLength.Star, 2)`:

```cs
// Add this using static to enable Columns.Define and Rows.Define 
using static CommunityToolkit.Maui.Markup.GridRowsColumns;

// ...

new Grid
{
    ColumnDefinitions = Columns.Define(30, Star, Stars(2)),
    RowDefinitions = Rows.Define(Auto, Star),

    Children = 
    {
        new Label()
            .Text("This Label is in Row 0 Column 0")
            .Row(0).Column(0)

        new Label()
            .Text("This Label is in Row 0 Column 1")
            .Row(0).Column(1)

        new Label()
            .Text("This Label is in Row 0 Column 2")
            .Row(1).Column(2)

        new Label()
            .Text("This Label is in Row 1 Column 0")
            .Row(1).Column(0)

        new Label()
            .Text("This Label is in Row 1 Column 1")
            .Row(1).Column(1)

        new Label()
            .Text("This Label is in Row 1 Column 2")
            .Row(1).Column(2)
    }
}
```

## Defining Rows + Columns Using Enums

We can also define and name our Rows and Columns by creating a custom `Enum`. Using an `Enum` allows us to define a name for each row and column making it easier to place our controls in the `Grid`.

### Example

The following example demonstrates how to define rows + columns for a `Grid` using two `Enum`s.

To leverage these helper methods, we first add the following `using static` directive:

```cs
using static CommunityToolkit.Maui.Markup.GridRowsColumns;
```

We then define the names of our Rows and Columns by creating a custom `Enum` for each:

```cs
enum Row { Username, Password, Submit }

enum Column { Description, UserInput }
```

We then then populate our `Grid` using these `Enum`s to define our rows + columns and to assign each control to a row + column accordingly:

```cs
using static CommunityToolkit.Maui.Markup.GridRowsColumns;

class LoginPage : ContentPage
{
    public LoginPage()
    {
        Content = new Grid
        {
            RowDefinitions = Rows.Define(
                (Row.Username, 30),
                (Row.Password, 30),
                (Row.Submit, Star)),
    
            ColumnDefinitions = Columns.Define(
                (Column.Description, Star),
                (Column.UserInput, Star)),
    
            Children = 
            {
                new Label()
                    .Text("Username")
                    .Row(Row.Username).Column(Column.Description),
    
                new Entry()
                    .Placeholder("Username")
                    .Row(Row.Username).Column(Column.UserInput),
    
                new Label()
                    .Text("Password")
                    .Row(Row.Password).Column(Column.Description),
    
                new Entry { IsPassword = true }
                    .Placeholder("Password")
                    .Row(Row.Password).Column(Column.UserInput),
    
                new Button()
                    .Text("Submit")
                    .Row(Row.Password).RowSpan(All<Column>())
            }
        }
    }

    enum Row { Username, Password, Submit }

    enum Column { Description, UserInput }
}
```

## Row

The `Row` method sets the `Grid.RowProperty` and `Grid.RowSpanProperty` on a `BindableObject`.

The following example sets the `Grid.RowProperty` of a `Button` to `0` and its `Grid.RowSpanProperty` to `2`, then sets the `Grid.RowProperty` of a `Label` to `1`:

```csharp
new Grid
{
    Children = 
    {
        new Button()
            .Text("This Button is in Row 0 and spans 2 Columns")
            .Row(0, 2),

        new Label()
            .Text("This Label is in Row 1 and does not span multiple columns")
            .Row(1)
    }
};
```

## Column

The `Column` method sets the `Grid.ColumnProperty` and `Grid.ColumnSpanProperty` on a `BindableObject`.

The following example sets the `Grid.ColumnProperty` of a `Button` to `0` and its `Grid.ColumnSpanProperty` to `2`, then sets the `Grid.ColumnProperty` of a `Label` to `1`:

```csharp
new Grid
{
    Children = 
    {
        new Button()
            .Text("This Button is in Row 0 and spans 2 Columns")
            .Column(0, 2),

        new Label()
            .Text("This Label is in Row 1 and does not span multiple columns")
            .Column(1)
    }
};
```

## RowSpan

The `RowSpan` method allows us to define how many Grid Rows a control will span across. I.e. If our `Grid` has 3 Rows, `.RowSpan(3)` will ensure the control spans across all 3 Columns.

Here's an example of a `Button` that spans vertically across 3 Rows:
```cs
new Button()
    .Text("This Button Spans Across 3 Grid Rows")
    .RowSpan(3)
```

### All&lt;TEnum>

When defining our Rows using an `Enum`, we can use `All<TEnum>()` to ensure our control spans vertically across every row:

```cs
enum Row { Username, Password, Submit }

// ...
new Button()
    .Text("This Button Spans Vertically Across Every Row Defined in our Enum")
    .RowSpan(All<Row>());
```

## ColumnSpan

The `ColumnSpan` method allows us to define how many Grid Columns a control will span across. I.e. If our `Grid` has 3 Columns, `.ColumnSpan(3)` will ensure the control spans across all 3 Columns.

Here's an example of a `Button` that spans horizontally across 3 Columns:
```cs
new Button()
    .Text("This Button Spans Across 3 Grid Columns")
    .ColumnSpan(3)
```

### All&lt;TEnum>

When defining our Rows using an `Enum`, we can use `All<TEnum>()` to ensure our control spans horizontally across every column:

```cs
enum Column { Description, UserInput }

// ...
new Button()
    .Text("This Button Spans Vertically Across Every Row Defined in our Enum")
    .ColumnSpan(All<Column>());
```

## Last&lt;TEnum>

When defining our rows and columns using an `Enum`, we can ensure a control is added to the last Row or the last Column by using `.Last<TEnum>()`.

This example demonstrates how to add a `Button` to the final row and column in a `Grid`

```cs
enum Row { Username, Password, Submit }
enum Column { Description, UserInput }

// ...
new Button()
    .Text("This Button Spans Vertically Across Every Row Defined in our Enum")
    .Row(Last<Row>()).Column(Last<Column>());
```
