---
title: CommunityToolkit.Maui.Options
author: VladislavAntonyuk
description: CommunityToolkit.Maui.Options allows to customize the CommunityToolkit.Maui.
ms.date: 09/14/2022
---

# CommunityToolkit.Maui.Options

`CommunityToolkit.Maui.Options` allows to customize the `CommunityToolkit.Maui`. The toolkit may behave different depends on these settings.

## SetShouldSuppressExceptionsInConverters

Allows to return default value instead of throwing an exception when using `BaseConverter{TFrom,TTo}`. Default value is false.

## SetShouldSuppressExceptionsInAnimations

Allows to return default value instead of throwing an exception when using `AnimationBehavior`. Default value is false.

## SetShouldSuppressExceptionsInBehaviors

Allows to return default value instead of throwing an exception when using `BaseBehavior{TView}`. Default value is false.