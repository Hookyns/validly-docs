---
icon: gear
---

# Configuration

## Project Configuration

You can configure the source generator via properties in your `csproj` or `Directory.build.props`.

```xml
<PropertyGroup>
    <ValigatorConfiguration>
        <AutoRequired>enabled</AutoRequired>
        <AutoInEnum>enabled</AutoInEnum>
    </ValigatorConfiguration>
</PropertyGroup>
```

### AutoRequire

The `AutoRequire` property allows you to automatically apply the `[Required]` attribute to your objects. When enabled, it ensures that all properties in your object that need to be non-nullable have this attribute applied. This makes it easier to enforce validation rules without manually adding the `[Required]` attribute to each property.&#x20;

This property is enabled by default. Use `<AutoRequired>disabled</AutoRequired>` in your project configuration to disable this feature.

### AutoInEnum

The `AutoInEnum` property allow you to automatically apply the \[InEnum] attribute to yout objects. When enabled, it ensures that all enum properties in your object have this attribute applied.&#x20;

This property is enabled by default. Use `<AutoInEnum>disabled</AutoInEnum>` in your project configuration to disable this feature.

## Override Project Configuration via Validatable Attribute

In addition to the global project configuration, you can use properties of the `[Validatable]` attribute to customize validation behavior on a per-object basis. The attribute provides two properties:

* `UseAutoValidators`: Enabling this option overrides the project configuration, applying automatic validators to the particular object even if they are disabled globally.
* `NoAutoValidators`: This option prevents the automatic validators from being applied, even if they are enabled by default in the project configuration.

These options offer flexibility, allowing you to fine-tune validation requirements for specific objects without altering the overall project settings.

```csharp
[Validatable(NoAutoValidators = true)]
public partial class CreateUserRequest
{
    public required string Username { get; init; }
}
```

## Runtime Options

To configure the runtime of the validation you can you static class `ValidlyOptions`.

```csharp
ValidlyOptions.Configure(cfg =>
    cfg.WithObjectPoolSize(16)
        .WithGlobalMessagesPoolSize(16)
        .WithPropertyMessagesPoolSize(16)
);
```



