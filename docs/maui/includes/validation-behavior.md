### ValidationBehavior Properties

The following properties are implemented in the base class, `public abstract class ValidationBehavior`:

|Property  |Type  |Description  |
|---------|---------|---------|
| `Flags` | `ValidationFlags` | Provides an enumerated value that specifies how to handle validation. |
| `ForceValidateCommand` | `ICommand` | Allows the user to provide a custom `ICommand` that handles forcing validation. |
| `InvalidStyle` | `Style` | The `Style` to apply to the element when validation fails. |
| `IsNotValid` | `bool` | Indicates whether or not the current value is considered not valid. |
| `IsRunning` | `bool` | Indicates whether or not the validation is in progress now (waiting for an asynchronous call is finished). |
| `IsValid` | `bool` | Indicates whether or not the current value is considered valid. |
| `ValidStyle` | `Style` | The `Style` to apply to the element when validation is successful. |
| `Value` | `object` | The value to validate. |
| `ValuePropertyName` | `string` | Allows the user to override the property that will be used as the value to validate. |