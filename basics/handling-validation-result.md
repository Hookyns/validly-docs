---
icon: list-check
---

# Handling Validation Result

The `ValidationResult` class represents the outcome of a validation process, encapsulating all validation messages and property-specific results. `ValidationResult` allows you to evaluate whether validation succeeded, access detailed validation messages, and work with property-specific outcomes.

```csharp
var request = new CreateUserRequest
{
    Username = "Brangelina",
    Password = "O6kNG1EDftZOWCf",
    Email = "john@example.com",
    Age = 30,
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

    foreach (var propertyResult in validationResult.Properties)
    {
        Console.WriteLine(
            $"{propertyResult.PropertyDisplayName} is "
                + (propertyResult.IsSuccess ? "VALID" : "INVALID:")
        );

        if (propertyResult.PropertyDisplayName != propertyResult.PropertyPath)
        {
            Console.WriteLine($"  property path: $.{propertyResult.PropertyPath}");
        }

        foreach (var message in propertyResult.Messages)
        {
            Console.WriteLine($"  - {string.Format(message.Message, message.Args)}");
        }
    }
}
```

Designed for performance and memory efficiency, `ValidationResult` utilizes a memory pool for allocation. Disposing of the object returns it to the pool, helping minimize unnecessary allocations and garbage collection overhead.

{% hint style="warning" %}
ValidationResult is Disposable!
{% endhint %}



### FAQ

#### Do I Have to Call Dispose?

`ValidationResult` is an object sourced from a memory pool. While disposing of it is recommended, it is not strictly required. When disposed, the `ValidationResult` is promptly returned to the pool. If not disposed, it will be handled by the Garbage Collector and resurrected during finalization. Although this ensures the object eventually returns to the pool, it can lead to unnecessary memory usage and increased overhead.

