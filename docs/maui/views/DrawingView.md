---
title: DrawingView - .NET MAUI Community Toolkit
author: VladislavAntonyuk
description: "The DrawingView allows to draw lines, save the image and restore it by settings the list of lines."
ms.date: 03/30/2022
---

# DrawingView

[!INCLUDE [docs under construction](../includes/preview-note.md)]

The `DrawingView` allows to draw lines, save the image and restore it by settings the list of lines.

> [!NOTE]
> The `DrawingView` is not supported on Windows until InkCanvas is migrated to WinUI 3.

## Syntax

The `DrawingView` is invoked using C#.

### XAML

```xml
<views:DrawingView
            x:Name="DrawingViewControl"
            Lines="{Binding MyLines}"
            MultiLineMode="true"
            ClearOnFinish="true"
            DrawingLineCompletedCommand="{Binding DrawingLineCompletedCommand}"
            DrawingLineCompleted="OnDrawingLineCompletedEvent"
            LineColor="Red"
            LineWidth="5"
            BackgroundColor="DarkGray"
            HorizontalOptions="FillAndExpand"
            VerticalOptions="FillAndExpand" />
```


### C#

```csharp
using CommunityToolkit.Maui.Views;

var gestureImage = new Image();
var drawingView = new DrawingView
{
    Lines = new ObservableCollection<DrawingLine>(),
    MultiLineMode = true,
    ClearOnFinish = false,
    DrawingLineCompletedCommand = new Command<DrawingLine>(line =>
    {
        var stream = line.GetImageStream(gestureImage.Width, gestureImage.Height, Colors.Gray);
        gestureImage.Source = ImageSource.FromStream(() => stream);
    }),
    LineColor = Colors.Red,
    LineWidth = 5,
    BackgroundColor = Colors.Red
};
drawingView.DrawingLineCompleted += (s, e) =>
{
    var stream = e.LastDrawingLine.GetImageStream(gestureImage.Width, gestureImage.Height, Colors.Gray);
    gestureImage.Source = ImageSource.FromStream(() => stream);
};

// get stream from lines collection
var lines = new List<DrawingLine>();
var stream1 = DrawingView.GetImageStream(
                lines,
                new Size(gestureImage.Width, gestureImage.Height),
                Colors.Black);

// get steam from the current DrawingView
var stream2 = drawingView.GetImageStream(gestureImage.Width, gestureImage.Height);
```

## Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| Lines | `ObservableCollection<DrawingLine>` | Collection of `DrawingLine` that are currently on the `DrawingView` |
| MultiLineMode | `bool` | Toggles multi-line mode. When true, multiple lines can be drawn on the `DrawingView` while the tap/click is released in-between lines. Note: when `ClearOnFinish` is also enabled, the lines are cleared after the tap/click is released. Additionally, `DrawingLineCompletedCommand` will be fired after each line that is drawn. |
| ClearOnFinish | `bool` | Indicates whether the `DrawingView` is cleared after releasing the tap/click and a line is drawn. Note: when `MultiLineMode` is also enabled, this might cause unexpected behavior. |
| DrawingLineCompletedCommand | `ICommand` | This command is invoked whenever the drawing of a line on the `DrawingView` has completed. Note that this is fired after the tap or click is lifted. When `MultiLineMode` is enabled this command is fired multiple times. |
| DrawingLineCompleted | `EventHandler<DrawingLineCompletedEventArgs>` | `DrawingView` event occurs when drawing line completed. |
| LineColor | `Color` | The color that is used by default to draw a line on the `DrawingView`. |
| LineWidth | `float` | The width that is used by default to draw a line on the `DrawingView`. |

### DrawingLine

The `DrawingLine` contains the list of points and allows configuring each line style individually.

#### Properties

|Property  |Type  |Description  |Default value
|---------|---------|---------|---------|
| LineColor | `Color` | The color that is used to draw the line on the `DrawingView`. | `Colors.Black` |
| LineWidth | `float` | The width that is used to draw the line on the `DrawingView`. | `5` |
| Points | `ObservableCollection<Point>` | The collection of `Point` that makes the line. | `new()` |
| Granularity | `int` | The granularity of this line. Min value is 5. The higher the value, the smoother the line, the slower the program.. | `5` |
| EnableSmoothedPath | `bool` | Enables or disables if this line is smoothed (anti-aliased) when drawn. | `false` |

### DrawingLineCompletedEventArgs

Event argument which contains last drawing line.

#### Properties

|Property  |Type  |Description  |
|---------|---------|---------|
| LastDrawingLine | `DrawingLine` | Last drawing line. |

## Methods

|Method  |Description  |
|---------|---------|
| GetImageStream | Retrieves a `Stream` containing an image of the `Lines` that are currently drawn on the `DrawingView`. |
| GetImageStream (static) | Retrieves a `Stream` containing an image of the collection of `DrawingLine` that is provided as a parameter. |

## Examples

You can find an example of this converter in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/DrawingViewPage.xaml.cs).

## API

You can find the source code for `DrawingView` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui/Views/DrawingView).
