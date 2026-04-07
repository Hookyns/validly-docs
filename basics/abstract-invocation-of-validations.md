---
icon: gallery-thumbnails
---

# Abstract Invocation of Validations

Every `[Validatable]` object automatically implements the `IValidatable` interface. This allows validation to be invoked from anywhere without needing to know signatures of the generated Validate() methods. The `IValidatable` interface standardizes validation calls across different objects.

```csharp
public interface IValidatable
{
    ValueTask<ValidationResult> ValidateAsync(IServiceProvider serviceProvider);
}
```

## Example Usage

Validation filter for the ASP.NET:

```csharp
public class ValidationFilter : IEndpointFilter
{
    private readonly IServiceProvider _serviceProvider;

    public ValidationFilter(IServiceProvider serviceProvider)
    {
        _serviceProvider = serviceProvider;
    }

    public async ValueTask<object?> InvokeAsync(
        EndpointFilterInvocationContext invocationContext,
        EndpointFilterDelegate next
    )
    {
        foreach (var argument in invocationContext.Arguments)
        {
            // Try to cast argument to IValidatable
            if (argument is IValidatable validatable)
            {
                // Invoke the validation
                var result = await validatable.Validate(_serviceProvider);

                if (!result.IsSuccess)
                {
                    return Results.Problem(...);
                }
            }
        }

        return await next(invocationContext);
    }
}
```



