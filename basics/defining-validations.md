---
icon: lightbulb-exclamation
---

# Defining Validations

Suppose you have a class representing an API request you want to validate:

```csharp
public class CreateUserRequest
{
    public required string Username { get; init; }
    public required string Password { get; init; }
    public required string Email { get; init; }
    public required int Age { get; init; }
    public string? FirstName { get; init; }
    public string? LastName { get; init; }
}
```

To enable validation capabilities, mark your DTO with the `[Validatable]` attribute and make it `partial`. This allows <mark style="color:purple;">**Validly**</mark> to generate a `Validate` instance method for the class.

```csharp
[Validatable]
public partial class CreateUserRequest
{
    // ...
}
```

Then, decorate each property with the appropriate validation attributes. Here’s an example:

```csharp
[LengthBetween(5, 20)] // Username must be between 5 and 20 characters.
public required string Username { get; init; }

[MinLength(12)] // Password must be at least 12 characters long.
public required string Password { get; init; }

[EmailAddress] // Email must be in a valid email format.
public required string Email { get; init; }

[Between(18, 120)] // Age must be between 18 and 120.
public required int Age { get; init; }

[NotEmpty] // First name, if provided, cannot be empty.
public string? FirstName { get; init; }

[NotEmpty] // Last name, if provided, cannot be empty.
public string? LastName { get; init; }
```

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden></th></tr></thead><tbody><tr><td><strong>Custom Property Validation Code</strong></td><td>Learn how to write custom code to validate a property</td><td></td></tr><tr><td><strong>Before and After Validate Hooks</strong></td><td>Learn how to hook into validation, how to write custom validation code of whole model, handle and/or replace validation result</td><td></td></tr></tbody></table>

