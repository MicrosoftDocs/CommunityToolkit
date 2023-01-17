---
title: MediaPlayer - .NET MAUI Community Toolkit
description: "This article explains how to use MediaPlayer to play video and audio in a .NET MAUI application."
author: jfversluis
ms.author: joverslu
ms.date: 01/17/2023
---

# MediaPlayer

`MediaPlayer` is a view for playing video and audio. Media that's supported by the underlying platform can be played from the following sources:

- The web, using a URI (HTTP or HTTPS).
- A resource embedded in the platform application, using the `embed://` URI scheme.
- Files that come from the app's local and temporary data folders, using the `filesystem://` URI scheme.
- The device's library.

`MediaPlayer` can use the platform playback controls, which are referred to as transport controls. However, they are disabled by default and can be replaced with your own transport controls. The following screenshots show `MediaPlayer` playing a video with the platform transport controls:

![Screenshot of a MediaPlayer playing a video, on iOS and Android.](mediaelement-images/playback-controls-large.png#lightbox)

> [!NOTE]
> `MediaPlayer` is available on iOS, Android, Windows, macOS, and Tizen.

<!-- TODO: Add info about supported formats. For information about supported media formats on Android, see [Supported media formats](https://developer.android.com/guide/topics/media/media-formats) on developer.android.com. For information about supported media formats on the Universal Windows Platform (UWP), see [Supported codecs](/windows/uwp/audio-video-camera/supported-codecs). -->

## Play remote media

A `MediaPlayer` can play remote media files using the HTTP and HTTPS URI schemes. This is accomplished by setting the `Source` property to the URI of the media file:

```xaml
<MediaPlayer Source="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4"
             ShouldShowPlaybackControls="True" />
```

> [!IMPORTANT]
> When playing remote sources from HTTP endpoints, you will likely need to disable operating system security measures that prevent access to insecure web endpoints. This is true for at least iOS and Android.

By default, the media that is defined by the `Source` property doesn't immediately start playing after the media is opened. To enable automatic media playback, set the `ShouldAutoPlay` property to `true`.

Platform provided media playback controls are enabled by default, and can be disabled by setting the `ShouldShowPlaybackControls` property to `false`.

## Play local media

Local media can be played from the following sources:

- A resource embedded in the platform application, using the `embed://` URI scheme.
- Files that come from the app's local and temporary data folders, using the `filesystem://` URI scheme.
<!-- TODO - The device's library. -->

### Play media embedded in the app package

A `MediaPlayer` can play media files that are embedded in the app package, using the `embed://` URI scheme. Media files are embedded in the app package by placing them in the platform project.

To enable a media file for playback from the local resources add the file to the `Resources/Raw` folder of you .NET MAUI project. When a file is added in the root, the URI would be `embed://MyFile.mp4`.

You can also place files in subfolders. If `MyFile.mp4` would be in `Resources/Raw/MyVideos` then the URI to use it with `MediaPlayer` would be `embed://MyVideos/MyFile.mp4`.

An example of how to use this syntax in XAML can be seen below.

```xaml
<MediaPlayer Source="embed://MyFile.mp4"
             ShouldShowPlaybackControls="True" />
```

<!-- When using data binding, a value converter can be used to apply this URI scheme:

```csharp
public class VideoSourceConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        if (value == null)
            return null;

        if (string.IsNullOrWhiteSpace(value.ToString()))
            return null;

        if (Device.RuntimePlatform == Device.UWP)
            return new Uri($"ms-appx:///Assets/{value}");
        else
            return new Uri($"ms-appx:///{value}");
    }
    // ...
}
```

An instance of the `VideoSourceConverter` can then be used to apply the `ms-appx:///` URI scheme to an embedded media file:

```xaml
<MediaPlayer Source="{Binding MediaSource, Converter={StaticResource VideoSourceConverter}}"
              ShowsPlaybackControls="True" />
```

For more information about the ms-appx URI scheme, see [ms-appx and ms-appx-web](/windows/uwp/app-resources/uri-schemes#ms-appx-and-ms-appx-web). -->

### Play media from the device library

Most modern mobile devices and desktop computers have the ability to record videos and audio using the device's camera and microphone. The media that's created are then stored as files on the device. These files can be retrieved from the library and played by the `MediaPlayer`.

Each of the platforms includes a facility that allows the user to select media from the device's library. In Xamarin.Forms, platform projects can invoke this functionality, and it can be called by the [`DependencyService`](xref:Xamarin.Forms.DependencyService) class.

The video picking dependency service used in the sample application is very similar to one defined in [Picking a Photo from the Picture Library](/xamarin/xamarin-forms/app-fundamentals/dependency-service/photo-picker), except that the picker returns a filename rather than a `Stream` object. The shared code project defines an interface named `IVideoPicker`, that defines a single method named `GetVideoFileAsync`. Each platform then implements this interface in a `VideoPicker` class.

The following code example shows how to retrieve a media file from the device library:

```csharp
string filename = await DependencyService.Get<IVideoPicker>().GetVideoFileAsync();
if (!string.IsNullOrWhiteSpace(filename))
{
    mediaElement.Source = new FileMediaSource
    {
        File = filename
    };
}
```

The video picking dependency service is invoked by calling the `DependencyService.Get` method to obtain the implementation of an `IVideoPicker` interface in the platform project. The `GetVideoFileAsync` method is then called on that instance, and the returned filename is used to create a `FileMediaSource` object and to set it to the `Source` property of the `MediaPlayer`.

<!--TODO ## Change video aspect ratio

The `Aspect` property determines how video media will be scaled to fit the display area. By default, this property is set to the `AspectFit` enumeration member, but it can be set to any of the [`Aspect`](xref:Xamarin.Forms.Aspect) enumeration members:

- `AspectFit` indicates that the video will be letterboxed, if required, to fit into the display area, while preserving the aspect ratio.
- `AspectFill` indicates that the video will be clipped so that it fills the display area, while preserving the aspect ratio.
- `Fill` indicates that the video will be stretched to fill the display area.-->

<!-- TODO ## Binding to the `Position` property

The property change notification for the `Position` bindable property fire at 200ms intervals while playing. Therefore, the property can be data-bound to a `Slider` control (or similar) to show progress through the media. The CommunityToolkit also provides a [`TimeSpanToDoubleConverter`](xref:Xamarin.CommunityToolkit.Converters.TimeSpanToDoubleConverter) which converts a [`TimeSpan`](xref:System.TimeSpan) into a floating point value representing total seconds elapsed. In this way you can set the Slider `Maximum` to the `Duration` of the media and the `Value` to the `Position` to provide accurate progress:

```xaml
<?xml version="1.0" encoding="UTF-8"?>
<pages:BasePage xmlns="http://xamarin.com/schemas/2014/forms"
                xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                xmlns:xct="http://xamarin.com/schemas/2020/toolkit"
                xmlns:pages="clr-namespace:Xamarin.CommunityToolkit.Sample.Pages"
                x:Class="Xamarin.CommunityToolkit.Sample.Pages.Views.MediaPlayerPage">
    <pages:BasePage.Resources>
        <xct:TimeSpanToDoubleConverter x:Key="TimeSpanConverter"/>
    </pages:BasePage.Resources>
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="*"/>
            <RowDefinition Height="*"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>
        <xct:MediaPlayer
            x:Name="mediaElement"
            Source="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4"
            ShowsPlaybackControls="True"
            HorizontalOptions="Fill"
            SeekCompleted="OnSeekCompleted" />
        <Slider Grid.Row="1" BindingContext="{x:Reference mediaElement}" Value="{Binding Position, Converter={StaticResource TimeSpanConverter}}" Maximum="{Binding Duration, Converter={StaticResource TimeSpanConverter}}">
            <Slider.Triggers>
                <DataTrigger TargetType="Slider"
                     Binding="{Binding CurrentState}"
                     Value="{x:Static MediaPlayerState.Buffering}">
                    <Setter Property="IsEnabled" Value="False" />
                </DataTrigger>
            </Slider.Triggers>
        </Slider>
        <Button Grid.Row="2" Text="Reset Source (Set Null)" Clicked="OnResetClicked" />
    </Grid>
</pages:BasePage>
```

In this example, the `Maximum` property of the `Slider` is data-bound to the `Duration` property of the `MediaPlayer` and the [`Value`](xref:Microsoft.Maui.Controls.Slider.Value) property of the [`Slider`](xref:Microsoft.Maui.Controls.Slider) is data-bound to the `Position` property of the `MediaPlayer`. Therefore, dragging the `Slider` results in the media playback position changing:

![Screenshot of a MediaPlayer with a position bar, on iOS and Android.](mediaelement-images/custom-position-bar-large.png#lightbox)

In addition, a [`DataTrigger`](xref:Microsoft.Maui.Controls.DataTrigger) object is used to disable the `Slider` when the media is buffering. For more information about data triggers, see [.NET MAUI Triggers](/dotnet/maui/fundamentals/triggers).

> [!NOTE]
> On Android, the [`Slider`](xref:Microsoft.Maui.Controls.Slider) only has 1000 discrete steps, regardless of the `Minimum` and `Maximum` settings. If the media length is greater than 1000 seconds, then two different `Position` values would correspond to the same `Value` of the `Slider`. This is why the code above checks that the new position and existing position are greater than one-hundredth of the overall duration. -->

## Understand MediaSource types

A `MediaPlayer` can play media by setting its `Source` property to a remote or local media file. The `Source` property is of type `MediaSource`, and this class defines three static methods:

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

## Determine `MediaPlayer` status

The `MediaPlayer` class defines a read-only bindable property named `CurrentState`, of type `MediaPlayerState`. This property indicates the current status of the control, such as whether the media is playing or paused, or if it's not yet ready to play the media.

The `MediaPlayerState` enumeration defines the following members:

- `None` indicates that the `MediaPlayer` contains no media.
- `Opening` indicates that the `MediaPlayer` is validating and attempting to load the specified source.
- `Buffering` indicates that the `MediaPlayer` is loading the media for playback. Its `Position` property does not advance during this state. If the `MediaPlayer` was playing video, it continues to display the last displayed frame.
- `Playing` indicates that the `MediaPlayer` is playing the media source.
- `Paused` indicates that the `MediaPlayer` does not advance its `Position` property. If the `MediaPlayer` was playing video, it continues to display the current frame.
- `Stopped` indicates that the `MediaPlayer` contains media but it is not being played or paused. Its `Position` property is reset to 0 and does not advance.
- `Failed` indicates that the `MediaPlayer` failed to load or play the media. This can occur while trying to load a new media item, when attempting to play the media item or when the media playback is interrupted due to a failure. Use the `MediaFailed` event to retrieve additional details.

It's generally not necessary to examine the `CurrentState` property when using the `MediaPlayer` transport controls. However, this property becomes important when implementing your own transport controls.

## Implement custom transport controls

The transport controls of a media player include the buttons that perform the functions **Play**, **Pause**, and **Stop**. These buttons are generally identified with familiar icons rather than text, and the **Play** and **Pause** functions are generally combined into one button.

By default, the `MediaPlayer` playback controls are disabled. This enables you to control the `MediaPlayer` programmatically, or by supplying your own transport controls. In support of this, `MediaPlayer` includes `Play`, `Pause`, and `Stop` methods.

The following XAML example shows a page that contains a `MediaPlayer` and custom transport controls:

```xaml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:toolkit="http://schemas.microsoft.com/dotnet/2022/maui/toolkit"
             x:Class="MediaPlayerDemos.CustomTransportPage"
             Title="Custom transport">
    <Grid>
        ...
        <toolkit:MediaPlayer x:Name="mediaPlayer"
                      ShouldAutoPlay="False"
                      ... />
        <HorizontalStackLayout BindingContext="{x:Reference mediaPlayer}"
                     ...>
            <Button Text="Play"
                    HorizontalOptions="CenterAndExpand"
                    Clicked="OnPlayPauseButtonClicked">
                <Button.Triggers>
                    <DataTrigger TargetType="Button"
                                 Binding="{Binding CurrentState}"
                                 Value="{x:Static toolkit:MediaPlayerState.Playing}">
                        <Setter Property="Text"
                                Value="Pause" />
                    </DataTrigger>
                    <DataTrigger TargetType="Button"
                                 Binding="{Binding CurrentState}"
                                 Value="{x:Static toolkit:MediaPlayerState.Buffering}">
                        <Setter Property="IsEnabled"
                                Value="False" />
                    </DataTrigger>
                </Button.Triggers>
            </Button>
            <Button Text="Stop"
                    HorizontalOptions="CenterAndExpand"
                    Clicked="OnStopButtonClicked">
                <Button.Triggers>
                    <DataTrigger TargetType="Button"
                                 Binding="{Binding CurrentState}"
                                 Value="{x:Static toolkit:MediaPlayerState.Stopped}">
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
    if (mediaPlayer.CurrentState == MediaPlayerState.Stopped ||
        mediaPlayer.CurrentState == MediaPlayerState.Paused)
    {
        mediaPlayer.Play();
    }
    else if (mediaPlayer.CurrentState == MediaPlayerState.Playing)
    {
        mediaPlayer.Pause();
    }
}

void OnStopButtonClicked(object sender, EventArgs args)
{
    mediaPlayer.Stop();
}
```

The **Play** button can be pressed, once it becomes enabled, to begin playback. Pressing the **Pause** button results in playback pausing. Pressing the **Stop** button stops playback and returns the position of the media file to the beginning.

## Implement a custom volume control

Media playback controls implemented by each platform include a volume bar. This bar resembles a slider and shows the volume of the media. In addition, you can manipulate the volume bar to increase or decrease the volume.

A custom volume bar can be implemented using a [`Slider`](xref:Microsoft.Maui.Controls.Slider), as shown in the following example:

```xaml
<StackLayout>
    <toolkit:MediaPlayer ShouldAutoPlay="False"
                         Source="{StaticResource AdvancedAsync}" />
    <Slider Maximum="1.0"
            Minimum="0.0"
            Value="{Binding Volume}"
            Rotation="270"
            WidthRequest="100" />
</StackLayout>
```

In this example, the [`Slider`](xref:Microsoft.Maui.Controls.Slider) data binds its `Value` property to the `Volume` property of the `MediaPlayer`. This is possible because the `Volume` property uses a `TwoWay` binding. Therefore, changing the `Value` property will result in the `Volume` property changing.

> [!NOTE]
> The `Volume` property has a validation callback that ensures that its value is greater than or equal to 0.0, and less than or equal to 1.0.

For more information about using a [`Slider`](xref:Microsoft.Maui.Controls.Slider) see, [.NET MAUI Slider](/dotnet/maui/user-interface/controls/slider)

## Properties

|Property  |Type  |Description  |Default Value  |
|---------|---------|---------|---------|
| CurrentState | `MediaPlayerState` | Indicates the current status of the control. This is a read-only, bindable property. | `MediaPlayerState.None` |
| Duration | `TimeSpan` | Indicates the duration of the currently opened media. This is a read-only, bindable property. | `TimeSpan.Zero` |
| Position | `TimeSpan` | Describes the current progress through the media's playback time. This is a read-only, bindable property. If you want to set the `Position` use the `SeekTo()` method. | `TimeSpan.Zero` |
| ShouldAutoPlay | `bool` | Indicates whether media playback will begin automatically when the `Source` property is set. This is a bindable property. | `false` |
| ShouldLoopPlayback | `bool` | Describes whether the currently loaded media source should resume playback from the start after reaching its end. This is a bindable property. | `false` |
| ShouldKeepScreenOn | `bool` | Determines whether the device screen should stay on during media playback. This is a bindable property. | `false` |
| ShouldShowPlaybackControls | `bool` | Determines whether the platforms playback controls are displayed. This is a bindable property. Note that on iOS and Windows the controls are only shown for a brief period after interacting with the screen. There is no way of keeping the controls visible at all times. | `true` |
| Source | `MediaSource?` | The source of the media loaded into the control. | `null` |
| Speed | `double` | Determines the playback speed of the media. This is a bindable property | `1` |
| MediaHeight | `int` | The height of the loaded media in pixels. This is a read-only, bindable property. | `0` |
| MediaWidth | `int` | The width of the loaded media in pixels. This is a read-only, bindable property. | `0` |
| Volume | `double` | Determines the media's volume, which is represented on a linear scale between 0 and 1. This is a bindable property. | `1` |

## Events

|Event  |Description  |
|---------|---------|
| MediaOpened | Occurs when the media stream has been validated and opened. |
| MediaEnded | Occurs when the `MediaPlayer` finishes playing its media. |
| MediaFailed | Occurs when there's an error associated with the media source. |
| PositionChanged | Occurs when the `Position` property value has changed. |
| SeekCompleted | Occurs when the seek point of a requested seek operation is ready for playback. |

## Methods

|Event  |Description  |
|---------|---------|
| Play | Starts playing the loaded media. |
| Pause | Pauses playback of the current media. |
| Stop | Stops playback and resets the position of the current media. |
| SeekTo | Takes a `TimeSpan` value to set the `Position` property to. |

## Related links

- [MediaPlayerDemos (sample)](/samples/xamarin/xamarin-forms-samples/userinterface-mediaelementdemos/)
- [URI schemes](/windows/uwp/app-resources/uri-schemes)
- [.NET MAUI Triggers](/dotnet/maui/fundamentals/triggers)
- [.NET MAUI Slider](/dotnet/maui/user-interface/controls/slider)
- [Android: Supported media formats](https://developer.android.com/guide/topics/media/media-formats)
- [UWP: Supported codecs](/windows/uwp/audio-video-camera/supported-codecs)
