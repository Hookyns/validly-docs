---
description: >-
  Welcome to the Validly Quickstart Guide! This page will help you get up and
  running with Validly in no time. By the end of this guide, you’ll have a basic
  understanding of how to validate your models
icon: bullseye-arrow
---

# Quickstart

## Install the Validly Packages

```bash
dotnet add package Validly
dotnet add package Validly.Extensions.Validators
dotnet add package Validly.SourceGenerator
```

For more install options visit [Installation ](installation.md)page.

## Add Validations to Your Class

Define a class you want to validate and annotate its properties with **validation attributes**. These attributes specify the validation rules.

```csharp
[Validatable]
public partial class CreateUserRequest
{
    [LengthBetween(5, 20)]
    public required string Username { get; init; }

    [MinLength(12)]
    public required string Password { get; init; }

    [EmailAddress]
    public required string Email { get; init; }

    [Between(18, 120)]
    public required int Age { get; init; }

    [NotEmpty]
    public string? FirstName { get; init; }

    [NotEmpty]
    public string? LastName { get; init; }
}
```

* **\[Validatable]**: Marks the class for Validly validation generation.
* **Validation Attributes**: Define specific rules (e.g., `Required`, `MinLength`, `Between`).

## Validate Your Data

Use the `Validate()` method, which is automatically generated by Validly, to validate an instance of your class.

```csharp
var request = new CreateUserArgs
{
    Username = "Brangelina",
    Password = "O6kNG1EDftZOWCf",
    Email = "john@example.com",
    Age = 30,
    Type = UserType.Personal,
};

// Call the .Validate() method. It returns ValidationResult which is Disposable!
using var validationResult = request.Validate();

if (validationResult.IsSuccess)
{
    Console.WriteLine("Validation succeeded!");
}
else
{
    foreach (var error in validationResult.Global)
    {
        Console.WriteLine($"Error: {error.Message}");
    }

    foreach (var propertyError in validationResult.Properties)
    {
        Console.WriteLine($"Property {propertyError.PropertyPath} failed:");
        foreach (var message in propertyError.Messages)
        {
            Console.WriteLine($"  - {string.Format(message.Message, message.Args)}");
        }
    }
}
```

## Add Custom Validation (Optional)

For added flexibility, you can annotate a property with the `[CustomValidation]` attribute. This tells Validly to generate an interface containing a method specifically for validating that property. You’re free to customize the method’s signature to suit your needs—Validly will automatically update the generated interface to reflect your changes.

```csharp
[EmailAddress]
[CustomValidation]
public string Email { get; init; }

IEnumerable<ValidationMessage> ICreateUserArgsCustomValidation.ValidateEmail()
{
    if (Email.Contains("spam"))
    {
        yield return new ValidationMessage(
            "Email cannot contain 'spam'.",
            "Validations.CreateUserArgs.Email.Errors.Spam"
        );
    }
}

```

{% hint style="info" %}
It is recommended to implement the generated interface explicitly to keep it hidden during regular use of the class, ensuring a cleaner and more intuitive API.
{% endhint %}

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

## Using BeforeValidate and AfterValidate Hooks (Optional)

For even more control over the validation process, Validly allows you to implement the `BeforeValidate` and `AfterValidate` methods within your class.

* **`BeforeValidate`**: Called before the validation process begins, allowing you to perform any pre-validation logic.
* **`AfterValidate`**: Called after the validation completes, allowing you to adjust the final validation result or add global messages.

```csharp
private void BeforeValidate()
{
    // Perform custom logic before validation starts
}

private ValidationResult AfterValidate(ValidationResult result)
{
    // Add global messages or adjust validation result after validation
    return result;
}
```

Both methods optionally accept a `ValidationContext` parameter, which is useful for scenarios where you need access to parent/root object. You can also use method parameters for dependency injection, allowing you to retrieve services directly from the service provider.

Return types for these methods are flexible and can include:

* `ValidationMessage?`
* `Validation`
* `IEnumerable<ValidationMessage>`
* `IAsyncEnumerable<ValidationMessage>`
* `Task<ValidationMessage?>`
* `Task<Validation>`
* `ValueTask<ValidationMessage?>`
* `ValueTask<Validation>`
* `void`
* `ValidationResult`

If you return a `ValidationResult`, the validation will stop immediately and return the provided result, bypassing any further validation steps.

### AfterValidate Method

In the `AfterValidate` method, you receive the `ValidationResult` or `ExtendableValidationResult` as a parameter. This allows you to manipulate the validation result after the validation process is complete. You can modify the existing result by adding or updating validation messages, changing the success state of properties, or adjusting other details. Alternatively, you can return a completely new validation result, overriding the original outcome if needed. This flexibility enables you to fine-tune the validation process or apply custom logic.
