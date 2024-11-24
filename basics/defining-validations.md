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

