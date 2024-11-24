# CustomValidation Attribute

Whenever custom logic is needed to validate a property — for instance, a complex condition involving multiple properties — you can use the `CustomValidationAttribute`. By adding `[CustomValidation]` to a property, an interface with a method specific to custom validation for that property will be generated, which you then implement within your Object. This method is called during validation just like standard validators. As an instance method, it provides access to the entire Object, allowing you to define any necessary conditions.

You’re free to customize the method’s signature to suit your needs—Validly will automatically update the generated interface to reflect your changes.

{% hint style="info" %}
It is recommended to implement the generated interface explicitly to keep it hidden during regular use of the class, ensuring a cleaner and more intuitive API.
{% endhint %}

{% code overflow="wrap" fullWidth="false" %}
```csharp
[Validatable]
public partial class CreateUserRequest
{
    [Required]
    [EmailAddress]
    [CustomValidation] // When added, the ICreateUserRequestCustomValidation is created
    public string Email { get; set; }

    IEnumerable<ValidationMessage> ICreateUserRequestCustomValidation.ValidateEmail()
    {
        // Here you can do whatever you want...
        if (Email.Contains("localhost"))
        {
            yield return new ValidationMessage(
                "Email cannot contain 'localhost'.",
                "Valigator.Validations.EmailAddress"
            );
        }
    }
}
```
{% endcode %}

#### Method Parameters

You can use method parameters for dependency injection, allowing you to retrieve services directly from the service provider.

#### Return Type

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

