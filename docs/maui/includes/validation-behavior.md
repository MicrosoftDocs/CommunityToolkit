---
ms.topic: include
---

### ValidationBehavior Properties

The following properties are implemented in the base class, `public abstract class ValidationBehavior`:

|Property  |Type  |Description  |
|---------|---------|---------|
| `Flags` | `ValidationFlags` | Provides an enumerated value that specifies how to handle validation. Once the behavior has validated a value, a change of a validation rule, of `ValidStyle`, of `InvalidStyle` or of `Flags` validates the current `Value` again, whatever the flags, so that `IsValid` follows the current rules. `ForceMakeValidWhenFocused` still keeps a focused view valid. |
| `ForceValidateCommand` | `ICommand` | Allows the user to provide a custom `ICommand` that handles forcing validation. |
| `InvalidStyle` | `Style` | The `Style` to apply to the element when validation fails. |
| `IsNotValid` | `bool` | Indicates whether or not the current value is considered not valid. |
| `IsRunning` | `bool` | Indicates whether or not the validation is in progress now (waiting for an asynchronous call is finished). |
| `IsValid` | `bool` | Indicates whether or not the current value is considered valid. |
| `ValidStyle` | `Style` | The `Style` to apply to the element when validation is successful. |
| `Value` | `object` | The value to validate. |
| `ValuePropertyName` | `string` | Allows the user to override the property that will be used as the value to validate. It must name a `BindableProperty`. For any other property, set it to `{x:Null}` first, then bind `Value` yourself. See [Trimming and Native AOT](../trimming-and-native-aot.md#validate-a-property-that-is-not-a-bindableproperty). |
