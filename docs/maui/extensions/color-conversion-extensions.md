---
title: ColorConversionExtensions - .NET MAUI Community Toolkit
author: bijington
description: "The ColorConversionExtensions provide a series of extension methods that support converting, modifying or inspecting Colors."
ms.date: 11/15/2026
---

# ColorConversionExtensions

The `ColorConversionExtensions` provide a series of extension methods that support converting, modifying or inspecting `Color`s.

The `ColorConversionExtensions` can be found under the `CommunityToolkit.Maui.Core.Extensions` namespace so just add the following line to get started:

```csharp
using CommunityToolkit.Maui.Core.Extensions;
```

## Convert Colors

The following methods allow you to convert the `Color`.

### ToBlackOrWhite

The `ToBlackOrWhite` method converts the `Color` to a monochrome value of `Colors.Black` or `Colors.White`.

The following example shows how to convert `Colors.Red` to a monochrome value:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.ToBlackOrWhite();
```

### ToBlackOrWhiteForText

The `ToBlackOrWhiteForText` method converts the `Color` to a monochrome value of `Colors.Black` or `Colors.White` based on whether the `Color` is determined as being dark for the human eye.

The following example shows how to convert `Colors.Red` to a monochrome value:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.ToBlackOrWhiteForText();
```

### ToGrayScale

The `ToGrayScale` method converts the `Color` to a gray scale `Color`.

The following example shows how to convert `Colors.Red` to a gray scale value:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.ToGrayScale();
```

### ToInverseColor

The `ToInverseColor` method inverts the `Color`.

The following example shows how to invert `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.ToInverseColor();
```

## Determining Color darkness

The following methods allow you to determine whether the `Color` is considered dark.

### IsDark

The `IsDark` method if the `Color` is dark.

The following example shows how to determine if `Colors.Red` is considered dark:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.IsDark();
```

### IsDarkForTheEye

The `IsDarkForTheEye` method if the `Color` is dark for the human eye.

The following example shows how to determine if `Colors.Red` is considered dark for the human eye:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.IsDarkForTheEye();
```

## Get Color components

The following methods allow you to obtain one of the components of the `Color`.

### GetByteRed

The `GetByteRed` method get the **red** component of `Color` as a value between 0 and 255.

The following example shows how to get the red component of `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.GetByteRed();
```

### GetByteGreen

The `GetByteGreen` method get the **green** component of `Color` as a value between 0 and 255.

The following example shows how to get the green component of `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.GetByteGreen();
```

### GetByteBlue

The `GetByteBlue` method get the **blue** component of `Color` as a value between 0 and 255.

The following example shows how to get the blue component of `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.GetByteBlue();
```

### GetDegreeHue

The `GetDegreeHue` method get the **hue** component of `Color` as a value between 0 and 360.

The following example shows how to get the hue component of `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.GetDegreeHue();
```

### GetPercentCyan

The `GetPercentCyan` method get the **cyan** component of `Color` as a value between 0 and 1.

The following example shows how to get the cyan component of `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.GetPercentCyan();
```

### GetPercentMagenta

The `GetPercentMagenta` method get the **magenta** component of `Color` as a value between 0 and 1.

The following example shows how to get the magenta component of `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.GetPercentMagenta();
```

### GetPercentYellow

The `GetPercentYellow` method get the **yellow** component of `Color` as a value between 0 and 1.

The following example shows how to get the yellow component of `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.GetPercentYellow();
```

### GetPercentBlackKey

The `GetPercentBlackKey` method get the **black key** component of `Color` as a value between 0 and 1.

The following example shows how to get the black key component of `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.GetPercentBlackKey();
```

### GetByteAlpha

The `GetByteAlpha` method get the **alpha** component of `Color` as a value between 0 and 255.

The following example shows how to get the alpha component of `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.GetByteAlpha();
```

## To Color string

The following methods allow you to convert the `Color` to a color scheme `string`.

### Culture

`ToCmykaString`, `ToCmykString`, `ToHslaString`, `ToHslString` and `ToRgbaString` format their numbers like this:

- No culture, or `null`: the documented, culture-invariant format on every machine, whatever `CultureInfo.CurrentCulture` is. For example `CMYK(0%,100%,100%,0%)` and `RGBA(255,0,0,0.5)`.
- `CultureInfo.InvariantCulture`, or a culture equal to it such as `new CultureInfo("")`: the same documented format. The percent sign follows the number (`100%`), where .NET's invariant culture writes `100 %`.
- Any other culture: the culture is honored. `tr-TR` writes `%100`, and `de-DE` and `uk-UA` write the alpha value `0.5` as `0,5`.

`ToRgbString` has no culture-dependent numbers.

> [!IMPORTANT]
> **Behavior change after v17.0.0:** without a culture, or with `null`, these methods now return the documented format on every machine. Through v17.0.0 they used `CultureInfo.CurrentCulture`, so on a `tr-TR` machine `Colors.Red.ToCmykString()` returned `CMYK(%0,%100,%100,%0)`, and on a `de-DE` machine `ToRgbaString()` returned `RGBA(255,0,0,0,5)` for an alpha of 0.5. Code that stores, compares or snapshot-tests these strings on non-English machines sees different text. Output on `en-US` machines doesn't change. To keep the old output, pass `CultureInfo.CurrentCulture`.

### ToCmykaString

The `ToCmykaString` method converts the `Color` to a `string` containing the cyan, magenta, yellow, key and alpha components. The resulting `string` will be in the format: `CMYKA(cyan,magenta,yellow,key,alpha)` where **cyan**, **magenta**, **yellow** and **key** will be a value between 0% and 100%, and **alpha** will be a value between 0 and 1 (e.g. `CMYKA(0%,100%,100%,0%,1)` for `Colors.Red`).

The following example shows how to convert `Colors.Red` to an CMYKA string:

```csharp
using CommunityToolkit.Maui.Core.Extensions;

Colors.Red.ToCmykaString();
```

Pass a culture to format the numbers with it, for example the **alpha** value with a different decimal separator:

```csharp
using System.Globalization;

new Color(0, 0, 0, 0.5f).ToCmykaString();                         // returns "CMYKA(0%,0%,0%,100%,0.5)" on every machine
new Color(0, 0, 0, 0.5f).ToCmykaString(new CultureInfo("en-US")); // returns "CMYKA(0%,0%,0%,100%,0.5)"
new Color(0, 0, 0, 0.5f).ToCmykaString(new CultureInfo("uk-UA")); // returns "CMYKA(0%,0%,0%,100%,0,5)"
```

### ToCmykString

The `ToCmykString` method converts the `Color` to a `string` containing the cyan, magenta, yellow and key components. The resulting `string` will be in the format: `CMYK(cyan,magenta,yellow,key)` where **cyan**, **magenta**, **yellow** and **key** will be a value between 0% and 100% (e.g. `CMYK(0%,100%,100%,0%)` for `Colors.Red`).

The following example shows how to convert `Colors.Red` to an CMYK string:

```csharp
using CommunityToolkit.Maui.Core.Extensions;

Colors.Red.ToCmykString();
```

Pass a culture to format the percentages with it:

```csharp
using System.Globalization;

Colors.Red.ToCmykString();                             // returns "CMYK(0%,100%,100%,0%)" on every machine
Colors.Red.ToCmykString(CultureInfo.InvariantCulture); // returns "CMYK(0%,100%,100%,0%)"
Colors.Red.ToCmykString(new CultureInfo("tr-TR"));     // returns "CMYK(%0,%100,%100,%0)"
```

### ToHslaString

The `ToHslaString` method converts the `Color` to a `string` containing the hue, saturation, lightness and alpha components. The resulting `string` will be in the format: `HSLA(hue,saturation,lightness,alpha)` where **hue** will be a value between 0 and 360, **saturation** and **lightness** will be a value between 0% and 100%, and **alpha** will be a value between 0 and 1 (e.g. `HSLA(360,100%,50%,1)` for `Colors.Red`).

The following example shows how to convert `Colors.Red` to an HSLA string:

```csharp
using CommunityToolkit.Maui.Core.Extensions;

Colors.Red.ToHslaString();
```

Pass a culture to format the numbers with it, for example the **alpha** value with a different decimal separator:

```csharp
using System.Globalization;

new Color(0, 0, 0, 0.5f).ToHslaString();                         // returns "HSLA(0,0%,0%,0.5)" on every machine
new Color(0, 0, 0, 0.5f).ToHslaString(new CultureInfo("en-US")); // returns "HSLA(0,0%,0%,0.5)"
new Color(0, 0, 0, 0.5f).ToHslaString(new CultureInfo("uk-UA")); // returns "HSLA(0,0%,0%,0,5)"
```

### ToHslString

The `ToHslString` method converts the `Color` to a `string` containing the hue, saturation and lightness components. The resulting `string` will be in the format: `HSL(hue,saturation,lightness)` where **hue** will be a value between 0 and 360, and **saturation** and **lightness** will be a value between 0% and 100% (e.g. `HSL(360,100%,50%)` for `Colors.Red`).

The following example shows how to convert `Colors.Red` to an HSL string:

```csharp
using CommunityToolkit.Maui.Core.Extensions;

Colors.Red.ToHslString();
```

Pass a culture to format the percentages with it:

```csharp
using System.Globalization;

Colors.Red.ToHslString();                         // returns "HSL(360,100%,50%)" on every machine
Colors.Red.ToHslString(new CultureInfo("tr-TR")); // returns "HSL(360,%100,%50)"
```

### ToRgbaString

The `ToRgbaString` method converts the `Color` to a `string` containing the red, green, blue and alpha components. The resulting `string` will be in the format: `RGBA(red,green,blue,alpha)` where **red**, **green** and **blue** will be a value between 0 and 255, and **alpha** will be a value between 0 and 1 (e.g. `RGBA(255,0,0,1)` for `Colors.Red`).

The following example shows how to convert `Colors.Red` to an RGBA string:

```csharp
using CommunityToolkit.Maui.Core.Extensions;

Colors.Red.ToRgbaString();
```

Pass a culture to format the numbers with it, for example the **alpha** value with a different decimal separator:

```csharp
using System.Globalization;

new Color(0, 0, 0, 0.5f).ToRgbaString();                         // returns "RGBA(0,0,0,0.5)" on every machine
new Color(0, 0, 0, 0.5f).ToRgbaString(new CultureInfo("en-US")); // returns "RGBA(0,0,0,0.5)"
new Color(0, 0, 0, 0.5f).ToRgbaString(new CultureInfo("uk-UA")); // returns "RGBA(0,0,0,0,5)"
```

### ToRgbString

The `ToRgbString` method converts the `Color` to a `string` containing the red, green and blue components. The resulting `string` will be in the format: `RGB(red,green,blue)` where **red**, **green** and **blue** will be a value between 0 and 255 (e.g. `RGB(255,0,0)` for `Colors.Red`).

The following example shows how to convert `Colors.Red` to an RGB string:

```csharp
using CommunityToolkit.Maui.Core.Extensions;

Colors.Red.ToRgbString();
```

## With Color components

The following methods allow you to replace one of the components of the `Color`.

### WithRed

The `WithRed` method applies the supplied `redComponent` to the `Color`. Note the `redComponent` can be a `double` between 0 and 1, or a `byte` between 0 and 255.

The following example shows how to apply the red component to `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.WithRed(0.5);
```

### WithGreen

The `WithGreen` method applies the supplied `greenComponent` to the `Color`. Note the `greenComponent` can be a `double` between 0 and 1, or a `byte` between 0 and 255.

The following example shows how to apply the green component to `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.WithGreen(0.5);
```

### WithBlue

The `WithBlue` method applies the supplied `blueComponent` to the `Color`. Note the `blueComponent` can be a `double` between 0 and 1, or a `byte` between 0 and 255.

The following example shows how to apply the blue component to `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.WithBlue(0.5);
```

### WithCyan

The `WithCyan` method applies the supplied `cyanComponent` to the `Color`. Note the `cyanComponent` must be a value between 0 and 1.

The following example shows how to apply the cyan component to `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.WithCyan(0.5);
```

### WithMagenta

The `WithMagenta` method applies the supplied `magentaComponent` to the `Color`. Note the `magentaComponent` must be a value between 0 and 1.

The following example shows how to apply the magenta component to `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.WithMagenta(0.5);
```

### WithYellow

The `WithYellow` method applies the supplied `yellowComponent` to the `Color`. Note the `yellowComponent` must be a value between 0 and 1.

The following example shows how to apply the yellow component to `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.WithYellow(0.5);
```

### WithBlackKey

The `WithBlackKey` method applies the supplied `blackKeyComponent` to the `Color`. Note the `blackKeyComponent` must be a value between 0 and 1.

The following example shows how to apply the black key component to `Colors.Red`:

```csharp
using CommunityToolkit.Maui.Extensions.Core;

Colors.Red.WithBlackKey(0.5);
```

## Examples

You can find an example of this extension in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Extensions/ColorConversionExtensionsPage.xaml).

## API

You can find the source code for `ColorConversionExtensions` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.Core/Extensions/ColorConversionExtensions.shared.cs).