# Creating Custom Validators

You can easily add custom validation by creating an attribute with an `IsValid` method that accepts the value to be validated as the first parameter. There is no need to implement any interface — just decorate your custom attribute with the `[Validator]` attribute, allowing the Source Generator to discover it easily (performance optimization).

Here's an example:

```csharp
[Validator]
[ValidatorDescription("must be one of the defined enum members")]
[AttributeUsage(AttributeTargets.Property)]
public class InEnumAttribute : Attribute
{
    private static readonly ValidationMessage ValidationMessage =
        new("Must be one of the defined enum members.", "Valigator.Validations.InEnum");

    public ValidationMessage? IsValid<TEnum>(TEnum value)
        where TEnum : struct, Enum
    {
        return !Enum.IsDefined(typeof(TEnum), value) ? ValidationMessage : null;
    }
}
```

{% hint style="info" %}
The `ValidatorDescription` attribute is optional but recommended. It serves as a description for your custom validation, making it easier to identify or document, especially if you want to list all validations on an API request object for documentation or user reference.
{% endhint %}

#### Method Parameters

You can use method parameters for dependency injection, allowing you to retrieve services directly from the service provider.

#### Return Value

The validation method supports a variety of return types, offering maximum flexibility to fit your workflow:

* **Single Message or Validation result**:
  * `ValidationMessage?`
  * `Validation.Error(), Validation.Success()`
* **Collection of Messages:**
  * `IEnumerable<ValidationMessage>`
* **Asynchronous Variants**:
  * `IAsyncEnumerable<ValidationMessage>`
  * `Task<ValidationMessage?>`
  * `Task<Validation>`
  * `ValueTask<ValidationMessage?>`
  * `ValueTask<Validation>`

This versatility means you can write validation logic synchronously or asynchronously, handle single errors or multiple.

