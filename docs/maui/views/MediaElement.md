---
title: MediaElement - .NET MAUI Community Toolkit
description: "This article explains how to use MediaElement to play video and audio in a .NET MAUI application."
author: jfversluis
ms.author: joverslu
ms.date: 02/15/2024
---

# MediaElement

`MediaElement` is a control for playing video and audio. Media that's supported by the underlying platform can be played from the following sources:

- The web, using a URI (HTTP or HTTPS).
- A resource embedded in the platform application, using the `embed://` URI scheme.
- Files that come from the app's local filesystem, using the `filesystem://` URI scheme.

`MediaElement` can use the platform playback controls, which are referred to as transport controls. However, they are disabled by default and can be replaced with your own transport controls. The following screenshots show `MediaElement` playing a video with the platform transport controls:

![Screenshot of a MediaElement playing a video, on Android and iOS.](../../images/mediaelement/intro.png#lightbox)

> [!NOTE]
> `MediaElement` is available on iOS, Android, Windows, macOS, and Tizen.

The `MediaElement` uses the following platform implementations.

|Platform| Platform media player implementation |
|--------|-----------------------|
| Android | [ExoPlayer](https://exoplayer.dev), big thank you to the [Android Libraries](https://github.com/dotnet/android-libraries) maintainers! |
| iOS/macOS | [AVPlayer](xref:AVFoundation.AVPlayer) |
| Windows | [MediaPlayer](xref:Windows.Media.Playback.MediaPlayer) |

## Getting started

To use the `MediaElement` feature of the .NET MAUI Community Toolkit, the following steps are required.

### Install NuGet package

Before you are able to use `MediaElement` inside your application you will need to install the `CommunityToolkit.Maui.MediaElement` NuGet package and add an initialization line in your *MauiProgram.cs*. As follows:

**Package name:** `CommunityToolkit.Maui.MediaElement`

**Package url:** https://www.nuget.org/packages/CommunityToolkit.Maui.MediaElement

### Initializing the package

First the using statement needs to be added to the top of your *MauiProgram.cs* file

```csharp
using CommunityToolkit.Maui.MediaElement;
```

In order to use the `MediaElement` correctly the `UseMauiCommunityToolkitMediaElement` method must be called on the `MauiAppBuilder` class when bootstrapping an application the *MauiProgram.cs* file. The following example shows how to perform this.

```csharp
var builder = MauiApp.CreateBuilder();
builder
    .UseMauiApp<App>()
    .UseMauiCommunityToolkitMediaElement()
```

For more information on how to do this, please refer to the [Get Started](../get-started.md?tabs=CommunityToolkitMauiMediaElement#adding-the-nuget-packages) page.

### Platform specific initialization

To access the `MediaElement` functionality, the following platform specific setup is required.

<!-- markdownlint-disable MD025 -->
### [Android](#tab/android)

When using `MediaElement` it is essential to perform the following steps:

#### 1. Add `ResizableActivity` and `Launchmode` to Activity

```csharp
[Activity(Theme = "@style/Maui.SplashTheme", ResizeableActivity = true, MainLauncher = true, LaunchMode = LaunchMode.SingleTask)]
public class MainActivity : MauiAppCompatActivity
{
}
```

For a full example of this method included in an application please refer to the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Platforms/Android/MainActivity.cs)

### [Mac Catalyst](#tab/mac)

Edit the `Info.plist` for `MacCatalyst` and add the following keys.
```csharp
<key>UIBackgroundModes</key>
<array>
    <string>bluetooth-central</string>
    <string>audio</string>
</array>
<key>NSLocalNetworkUsageDescription</key>
<string></string>
```

### [iOS](#tab/ios)

Edit the `Info.plist` for `iOS` and add the following keys.
```csharp
<key>UIBackgroundModes</key>
<array>
    <string>audio</string>
</array>
```

### [Windows](#tab/windows)

No setup is required.


### [Tizen](#tab/tizen)

No setup is required.

-----
<!-- markdownlint-enable MD025 -->

## Supported Formats

The supported multimedia formats can be different per platform. In some cases it can even be dependant on what decoders are available or installed on the operating system that is used while running your app. For more detailed information on which formats are supported on each platform, please refer to the links below.

|Platform| Link | Notes |
|--------|------|-------|
| Android | [ExoPlayer Supported Formats](https://developer.android.com/guide/topics/media/exoplayer/supported-formats) | |
| iOS/macOS | [iOS/macOS Supported Formats](https://stackoverflow.com/a/45898816/1506387) | No official documentation on this exists |
| Windows | [Windows Supported Formats](/windows/uwp/audio-video-camera/supported-codecs) | On Windows the supported formats are very much dependent on what codecs are installed on the user's machine |
| Tizen | [Tizen Supported Formats](https://docs.tizen.org/application/native/tutorials/feature/app-multimedia-video) | |

> [!IMPORTANT]
> If the user is using a Windows N edition, no video playback is supported by default. Windows N editions have no video playback formats installed by design.

## Common scenarios

The following sections covers common usage scenarios for the `MediaElement`.

### Play remote media

A `MediaElement` can play remote media files using the HTTP and HTTPS URI schemes. This is accomplished by setting the `Source` property to the URI of the media file:

```xaml
<toolkit:MediaElement Source="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4"
              ShouldShowPlaybackControls="True" />
```

> [!IMPORTANT]
> When playing remote sources from HTTP endpoints, you will likely need to disable operating system security measures that prevent access to insecure web endpoints. This is true for at least iOS and Android.

By default, the media that is defined by the `Source` property doesn't immediately start playing after the media is opened. To enable automatic media playback, set the `ShouldAutoPlay` property to `true`.

Platform provided media playback controls are enabled by default, and can be disabled by setting the `ShouldShowPlaybackControls` property to `false`.

### Using Metadata

A `MediaElement` can use metadata for `MediaElement.MetadataTitle`, `MediaElement.MetadataArtist` and `MediaElement.MetadataArtworkUrl`. You can set
the title or artist to show what is currently playing on lockscreen controls for Windows, Mac Catalyst, iOS, and Android. You can set a local or 
remote URL with artwork for the lockscreen. It should be at least 1080P for best quality to be displayed. It must be a URL and be either `.jpg` or
 `.png` 

```xaml
<toolkit:MediaElement 
    MetadataTitle="Title"
    MetadataArtist="Artist"
    MetadataArtworkUrl= "http://www.myownpersonaldomain.com/image.jpg" />
```

```csharp
    MediaElement.MetadataTitle="Title";
    MediaElement.MetadataArtist="Artist";
    MediaElement.MetadataArtworkUrl= MediaSource.FromUri("http://www.myownpersonaldomain.com/image.jpg"); 
```

> [!IMPORTANT]
> You can set the metadata in either XAML or code behind. MetaData for artwork uses `MediaSource` to set source for artwork. You can use File Resource,
a Url or embedded image from App Package. If you are setting it in code behind you need to set the source in code behind. The source should
be set last. If you set the metadata in XAML or in constructor this note can be safely ignored.

### Using TextureView

A `MediaElement` can use `TextureView` on Android Platform. The platform default behavior is to use `SurfaceView`. Using Texture View adds support
to allow transparencies and other effects. This is set by changing the builder to use

```csharp
.UseMauiCommunityToolkitMediaElement(static options => 
{
				options.SetDefaultAndroidViewType(AndroidViewType.TextureView);
})
```

You can set `TextureView` for each media element you use as well. It can be set in `XAML` and codebehind. Using it this way will override the builder command `.UseMauiCommunityToolkitMediaElement()`.

```csharp
var mediaElement = new MediaElement
{
    AndroidViewType = AndroidViewType.TextureView
}
```

```xaml
<toolkit:MediaElement AndroidViewType="TextureView" />
```

> [!IMPORTANT]
> We do not recommend using TextureView unless you have a specific need for it. It has possible performance related issues if enabled and is recommended only for those that need transparencies and other advanced features.

### Play local media

Local media can be played from the following sources:

- A resource embedded in the platform application, using the `embed://` URI scheme.
- Files that come from the app's local filesystem, using the `filesystem://` URI scheme.

> [!NOTE]
> The shorthand `embed://` and `filesystem://` only work from XAML. In code, please use `MediaSource.FromResource()` and `MediaSource.FromFile()` respectively. Using these methods, you can omit the the `embed://` and `filesystem://` prefixes. The rest of the path should be the same.

### Play media embedded in the app package

A `MediaElement` can play media files that are embedded in the app package, using the `embed://` URI scheme. Media files are embedded in the app package by placing them in the platform project.

To enable a media file for playback from the local resources add the file to the `Resources/Raw` folder of your .NET MAUI project. When a file is added in the root, the URI would be `embed://MyFile.mp4`.

You can also place files in sub folders. If `MyFile.mp4` would be in `Resources/Raw/MyVideos` then the URI to use it with `MediaElement` would be `embed://MyVideos/MyFile.mp4`.

An example of how to use this syntax in XAML can be seen below.

```xaml
<toolkit:MediaElement Source="embed://MyFile.mp4"
              ShouldShowPlaybackControls="True" />
```

## Understand MediaSource types

A `MediaElement` can play media by setting its `Source` property to a remote or local media file. The `Source` property is of type `MediaSource`, and this class defines three static methods:

- `FromFile`, returns a `FileMediaSource` instance from a `string` argument.
- `FromUri`, returns a `UriMediaSource` instance from a `Uri` argument.
- `FromResource`, returns a `ResourceMediaSource` instance from a `string` argument.

In addition, the `MediaSource` class also has implicit operators that return `MediaSource` instances from `string` and `Uri` arguments.

> [!NOTE]
> When the `Source` property is set in XAML, a type converter is invoked to return a `MediaSource` instance from a `string` or `Uri`.

The `MediaSource` class also has these derived classes:

- `FileMediaSource`, which is used to specify a local media file from a `string`. This class has a `Path` property that can be set to a `string`. In addition, this class has implicit operators to convert a `string` to a `FileMediaSource` object, and a `FileMediaSource` object to a `string`.
- `UriMediaSource`, which is used to specify a remote media file from a URI. This class has a `Uri` property that can be set to a `Uri`.
- `ResourceMediaSource`, which is used to specify an embedded file that is provided through the app's resource files. This class has a `Path` property that can be set to a `string`.

> [!NOTE]
> When a `FileMediaSource` object is created in XAML, a type converter is invoked to return a `FileMediaSource` instance from a `string`.

## Change video aspect ratio

The `Aspect` property determines how video media will be scaled to fit the display area. By default, this property is set to the `AspectFit` enumeration member, but it can be set to any of the [`Aspect`](xref:Microsoft.Maui.Aspect) enumeration members:

- `AspectFit` indicates that the video will be letterboxed, if required, to fit into the display area, while preserving the aspect ratio.
- `AspectFill` indicates that the video will be clipped so that it fills the display area, while preserving the aspect ratio.
- `Fill` indicates that the video will be stretched to fill the display area.

## Determine `MediaElement` status

The `MediaElement` class defines a read-only bindable property named `CurrentState`, of type `MediaElementState`. This property indicates the current status of the control, such as whether the media is playing or paused, or if it's not yet ready to play the media.

The `MediaElementState` enumeration defines the following members:

- `None` indicates that the `MediaElement` contains no media.
- `Opening` indicates that the `MediaElement` is validating and attempting to load the specified source.
- `Buffering` indicates that the `MediaElement` is loading the media for playback. Its `Position` property does not advance during this state. If the `MediaElement` was playing video, it continues to display the last displayed frame.
- `Playing` indicates that the `MediaElement` is playing the media source.
- `Paused` indicates that the `MediaElement` does not advance its `Position` property. If the `MediaElement` was playing video, it continues to display the current frame.
- `Stopped` indicates that the `MediaElement` contains media but it is not being played or paused. Its `Position` property is reset to 0 and does not advance.
- `Failed` indicates that the `MediaElement` failed to load or play the media. This can occur while trying to load a new media item, when attempting to play the media item or when the media playback is interrupted due to a failure. Use the `MediaFailed` event to retrieve additional details.

It's generally not necessary to examine the `CurrentState` property when using the `MediaElement` transport controls. However, this property becomes important when implementing your own transport controls.

## Implement custom transport controls

The transport controls of a media player include the buttons that perform the functions **Play**, **Pause**, and **Stop**. These buttons are generally identified with familiar icons rather than text, and the **Play** and **Pause** functions are generally combined into one button.

By default, the `MediaElement` playback controls are disabled. This enables you to control the `MediaElement` programmatically, or by supplying your own transport controls. In support of this, `MediaElement` includes `Play`, `Pause`, and `Stop` methods.

The following XAML example shows a page that contains a `MediaElement` and custom transport controls:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MediaElementDemos.CustomTransportPage"
             Title="Custom transport">
    <Grid>
        ...
        <toolkit:MediaElement x:Name="mediaElement"
                      ShouldAutoPlay="False"
                      ... />
        <HorizontalStackLayout BindingContext="{x:Reference mediaElement}"
                     ...>
            <Button Text="Play"
                    HorizontalOptions="Center"
                    Clicked="OnPlayPauseButtonClicked">
                <Button.Triggers>
                    <DataTrigger TargetType="Button"
                                 Binding="{Binding CurrentState}"
                                 Value="{x:Static toolkit:MediaElementState.Playing}">
                        <Setter Property="Text"
                                Value="Pause" />
                    </DataTrigger>
                    <DataTrigger TargetType="Button"
                                 Binding="{Binding CurrentState}"
                                 Value="{x:Static toolkit:MediaElementState.Buffering}">
                        <Setter Property="IsEnabled"
                                Value="False" />
                    </DataTrigger>
                </Button.Triggers>
            </Button>
            <Button Text="Stop"
                    HorizontalOptions="Center"
                    Clicked="OnStopButtonClicked">
                <Button.Triggers>
                    <DataTrigger TargetType="Button"
                                 Binding="{Binding CurrentState}"
                                 Value="{x:Static toolkit:MediaElementState.Stopped}">
                        <Setter Property="IsEnabled"
                                Value="False" />
                    </DataTrigger>
                </Button.Triggers>
            </Button>
        </HorizontalStackLayout>
    </Grid>
</ContentPage>
```

In this example, the custom transport controls are defined as [`Button`](xref:Microsoft.Maui.Controls.Button) objects. However, there are only two `Button` objects, with the first `Button` representing **Play** and **Pause**, and the second `Button` representing **Stop**. [`DataTrigger`](xref:Microsoft.Maui.Controls.DataTrigger) objects are used to enable and disable the buttons, and to switch the first button between **Play** and **Pause**. For more information about data triggers, see [.NET MAUI Triggers](/dotnet/maui/fundamentals/triggers).

The code-behind file has the handlers for the [`Clicked`](xref:Microsoft.Maui.Controls.Button.Clicked) events:

```csharp
void OnPlayPauseButtonClicked(object sender, EventArgs args)
{
    if (mediaElement.CurrentState == MediaElementState.Stopped ||
        mediaElement.CurrentState == MediaElementState.Paused)
    {
        mediaElement.Play();
    }
    else if (mediaElement.CurrentState == MediaElementState.Playing)
    {
        mediaElement.Pause();
    }
}

void OnStopButtonClicked(object sender, EventArgs args)
{
    mediaElement.Stop();
}
```

The **Play** button can be pressed, once it becomes enabled, to begin playback. Pressing the **Pause** button results in playback pausing. Pressing the **Stop** button stops playback and returns the position of the media file to the beginning.

## Implement a custom volume control

Media playback controls implemented by each platform include a volume bar. This bar resembles a slider and shows the volume of the media. In addition, you can manipulate the volume bar to increase or decrease the volume.

A custom volume bar can be implemented using a [`Slider`](xref:Microsoft.Maui.Controls.Slider), as shown in the following example:

```xaml
<StackLayout>
    <toolkit:MediaElement ShouldAutoPlay="False"
                          Source="{StaticResource AdvancedAsync}" />
    <Slider Maximum="1.0"
            Minimum="0.0"
            Value="{Binding Volume}"
            Rotation="270"
            WidthRequest="100" />
</StackLayout>
```

In this example, the [`Slider`](xref:Microsoft.Maui.Controls.Slider) data binds its `Value` property to the `Volume` property of the `MediaElement`. This is possible because the `Volume` property uses a `TwoWay` binding. Therefore, changing the `Value` property will result in the `Volume` property changing.

> [!NOTE]
> The `Volume` property has a validation callback that ensures that its value is greater than or equal to 0.0, and less than or equal to 1.0.

For more information about using a [`Slider`](xref:Microsoft.Maui.Controls.Slider) see, [.NET MAUI Slider](/dotnet/maui/user-interface/controls/slider)

## Properties

|Property  |Type  |Description  |Default Value  |
|---------|---------|---------|---------|
| Aspect | [Aspect](xref:Microsoft.Maui.Aspect) | Determines the scaling mode for the (visual) media that is currently loaded. This is a bindable property. | `Aspect.AspectFit` |
| CurrentState | `MediaElementState` | Indicates the current status of the control. This is a read-only, bindable property. | `MediaElementState.None` |
| Duration | `TimeSpan` | Indicates the duration of the currently opened media. This is a read-only, bindable property. | `TimeSpan.Zero` |
| MetadataArtist | `string` | The name of the artist of the media source. |
| MetadataArtworkUrl | `MediaSource` | Sets the artwork for media source. | 
| MetadataTitle | `string` | Sets the Title of the media source. |
| Position | `TimeSpan` | Describes the current progress through the media's playback time. This is a read-only, bindable property. If you want to set the `Position` use the `SeekTo()` method. | `TimeSpan.Zero` |
| ShouldAutoPlay | `bool` | Indicates whether media playback will begin automatically when the `Source` property is set. This is a bindable property. | `false` |
| ShouldLoopPlayback | `bool` | Describes whether the currently loaded media source should resume playback from the start after reaching its end. This is a bindable property. | `false` |
| ShouldKeepScreenOn | `bool` | Determines whether the device screen should stay on during media playback. This is a bindable property. | `false` |
| ShouldMute | `bool` | Determines whether the audio is currently muted. This is a bindable property. | `false` |
| ShouldShowPlaybackControls | `bool` | Determines whether the platforms playback controls are displayed. This is a bindable property. Note that on iOS and Windows the controls are only shown for a brief period after interacting with the screen. There is no way of keeping the controls visible at all times. | `true` |
| Source | `MediaSource?` | The source of the media loaded into the control. | `null` |
| Speed | `double` | Determines the playback speed of the media. This is a bindable property | `1` |
| MediaHeight | `int` | The height of the loaded media in pixels. This is a read-only, bindable property. Not reported for non-visual media and might not always be populated on iOS/macOS for live streamed content. | `0` |
| MediaWidth | `int` | The width of the loaded media in pixels. This is a read-only, bindable property. Not reported for non-visual media and might not always be populated on iOS/macOS for live streamed content. | `0` |
| Volume | `double` | Determines the media's volume, which is represented on a linear scale between 0 and 1. This is a bindable property. | `1` |

## Events

|Event  |Description  |
|---------|---------|
| MediaOpened | Occurs when the media stream has been validated and opened. |
| MediaEnded | Occurs when the `MediaElement` finishes playing its media. |
| MediaFailed | Occurs when there's an error associated with the media source. |
| PositionChanged | Occurs when the `Position` property value has changed. |
| SeekCompleted | Occurs when the seek point of a requested seek operation is ready for playback. |

## Methods

|Event  |Description  |
|---------|---------|
| Play | Starts playing the loaded media. |
| Pause | Pauses playback of the current media. |
| Stop | Stops playback and resets the position of the current media. |
| SeekTo | Takes a `TimeSpan` value to set the `Position` property to and takes a `CancellationToken` to cancel the `Task`. |

## Examples

You can find examples of this control in action in the [.NET MAUI Community Toolkit Sample Application](https://github.com/CommunityToolkit/Maui/blob/main/samples/CommunityToolkit.Maui.Sample/Pages/Views/MediaElement).

## API

You can find the source code for `MediaElement` over on the [.NET MAUI Community Toolkit GitHub repository](https://github.com/CommunityToolkit/Maui/blob/main/src/CommunityToolkit.Maui.MediaElement/MediaElement.shared.cs).

## Related links

- [.NET MAUI Triggers](/dotnet/maui/fundamentals/triggers)
- [.NET MAUI Slider](/dotnet/maui/user-interface/controls/slider)
- [Android ExoPlayer: Supported media formats](https://exoplayer.dev/supported-formats.html)
- [iOS: Supported media formats](https://stackoverflow.com/a/45898816/1506387)
- [Windows: Supported codecs](/windows/uwp/audio-video-camera/supported-codecs)
- [Android ExoPlayer Bindings](https://github.com/Baseflow/ExoPlayerXamarin)
