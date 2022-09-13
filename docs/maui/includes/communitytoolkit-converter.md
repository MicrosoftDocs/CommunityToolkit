### BaseConverter Properties

The following properties are implemented in the base class, `public abstract class BaseConverter`:

|Property |Description  |
|---------|---------|
| `DefaultConvertReturnValue` | Default value to return when `IValueConverter.Convert(object?, Type, object?, CultureInfo?)` throws an `Exception`. This value is used when [CommunityToolkit.Maui.Options](../options.md)`.ShouldSuppressExceptionsInConverters` is set to `true`. |
| `DefaultConvertBackReturnValue` | Default value to return when `IValueConverter.ConvertBack(object?, Type, object?, CultureInfo?)` throws an `Exception`. This value is used when [CommunityToolkit.Maui.Options](../options.md)`.ShouldSuppressExceptionsInConverters` is set to `true`. |

### ICommunityToolkitValueConverter Properties

The following properties are implemented in the `public interface ICommunityToolkitValueConverter`:

|Property |Type     |Description  |
|---------|---------|---------|
| `DefaultConvertReturnValue` | `object?` | Default value to return when `IValueConverter.Convert(object?, Type, object?, CultureInfo?)` throws an `Exception`. This value is used when [CommunityToolkit.Maui.Options](../options.md)`.ShouldSuppressExceptionsInConverters` is set to `true`. |
| `DefaultConvertBackReturnValue` | `object?` | Default value to return when `IValueConverter.ConvertBack(object?, Type, object?, CultureInfo?)` throws an `Exception`. This value is used when [CommunityToolkit.Maui.Options](../options.md)`.ShouldSuppressExceptionsInConverters` is set to `true`. |