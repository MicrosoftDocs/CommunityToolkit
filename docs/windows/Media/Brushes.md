---
title: Brushes
author: erinwoo  
description: Brush effects that can be applied to images and backgrounds.
keywords: brush, acrylic, acrylicbrush, backdrop, blur, gamma, transfer, invert, saturation, sepia, tiles, tile, image, blend, brushes
dev_langs:
  - csharp
category: Xaml
subcategory: Effects
discussion-id: 0
issue-id: 0
icon: Assets/MediaBrushes.png
---

# Brushes

A brush object is used to paint graphical objects in XAML and can be layered with other visual elements such as images and backgrounds. For examples and further explanation of drawing concepts represented by Brush, see [Use brushes](/en-us/windows/uwp/graphics/using-brushes).

## AcrylicBrush

Acrylic is a type of Brush that creates a translucent texture. You can apply acrylic to app surfaces to add depth and help establish a visual hierarchy.
To learn more about the acrylic material in Windows: [link](/en-us/windows/apps/design/style/acrylic)

:::code language="xaml" source="~/../code-windows/components/Media/samples/Brushes/AcrylicBrushSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Media/samples/Brushes/AcrylicBrushSample.xaml.cs":::

#### *UWP only:*
There are two modes for setting the BackgroundSource property when using an `AcrylicBrush`.
Setting it to `Backdrop` results in the acrylic effect being applied to whatever is *behind the brush* in the application.

Setting BackgroundSource to `HostBackdrop` results in the acrylic effect being applied *behind the current application*.

## BackdropBlurBrush

A brush that blurs the background in the application.

:::code language="xaml" source="~/../code-windows/components/Media/samples/Brushes/BackdropBlurBrushSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Media/samples/Brushes/BackdropBlurBrushSample.xaml.cs":::

## BackdropGammaTransferBrush

A brush which modifies the color values of the brush's background in the application. Map the color intensities of an image using a gamma function created using an amplitude, exponent, and offset you provide for each channel.

:::code language="xaml" source="~/../code-windows/components/Media/samples/Brushes/BackdropGammaTransferBrushSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Media/samples/Brushes/BackdropGammaTransferBrushSample.xaml.cs":::

## BackdropInvertBrush

A brush that inverts the colors of the brush's background in the application.

:::code language="xaml" source="~/../code-windows/components/Media/samples/Brushes/BackdropInvertBrushSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Media/samples/Brushes/BackdropInvertBrushSample.xaml.cs":::

## BackdropSaturationBrush

A brush that can increase or decrease the saturation of the brush's background in the application. The `Saturation` property specifies a double value for the amount of Saturation to apply from 0.0 - 1.0. Zero being monochrome, and one being fully saturated. The default is 0.5.

:::code language="xaml" source="~/../code-windows/components/Media/samples/Brushes/BackdropSaturationBrushSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Media/samples/Brushes/BackdropSaturationBrushSample.xaml.cs":::

## BackdropSepiaBrush

A brush that applies the sepia effect to the brush's background. The `Intensity` property specifies a double value for the amount of Sepia to apply from 0.0 - 1.0. Zero being none, and one being full Sepia effect. The default is 0.5.

:::code language="xaml" source="~/../code-windows/components/Media/samples/Brushes/BackdropSepiaBrushSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Media/samples/Brushes/BackdropSepiaBrushSample.xaml.cs":::

## ImageBlendBrush

A brush that blends the provided image with whatever is behind it in the application with the provided blend mode. The ImageBlendMode property specifies how the image should be blended with the backdrop. More info about the effect modes can be found [here](https://microsoft.github.io/Win2D/WinUI2/html/T_Microsoft_Graphics_Canvas_Effects_BlendEffectMode.htm).

:::code language="xaml" source="~/../code-windows/components/Media/samples/Brushes/ImageBlendBrushSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Media/samples/Brushes/ImageBlendBrushSample.xaml.cs":::

## TilesBrush

A brush can be used to display a tiled image as a background.

:::code language="xaml" source="~/../code-windows/components/Media/samples/Brushes/TilesBrushSample.xaml":::

:::code language="csharp" source="~/../code-windows/components/Media/samples/Brushes/TilesBrushSample.xaml.cs":::


