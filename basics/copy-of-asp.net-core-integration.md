---
hidden: true
icon: wave-sine
---

# Copy of ASP.NET Core Integration

## Installation

{% tabs %}
{% tab title=".NET CLI" %}
```sh
dotnet add package Validly.Extensions.AspNetCore
```
{% endtab %}

{% tab title="Package Manager Console" %}
```powershell
Install-Package Validly.Extensions.AspNetCore
```
{% endtab %}

{% tab title="PackageReference" %}
```xml
<PackageReference Include="Validly.Extensions.AspNetCore" Version="1.3.0" />
```
{% endtab %}
{% endtabs %}

## Using Minimal API Filter

There is the `ValidlyValidationFilter` that can be applied on minimal API endpoints and groups.

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

var group = app.MapGroup("/api/users")
    // Adds ValidlyValidationFilter on a group
    .WithValidlyValidation(); // <-- just add this to specific endpoint or group

// Example group endpoint
group.MapPost(
    "",
    (CreateUserRequest request) =>
    {
        // ...
    }
);
```

## Using Middleware

Work in progress...

## ASP.NET Core Localization

Some extensions provided by this <mark style="color:purple;">Validly.Extensions.AspNetCore</mark> package needs to turn `ValidationMessage` into string (basicaly because of ModelState). To support this, <mark style="color:purple;">Validly</mark> uses ASP.NET's [RequestLocalizationOptions](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/localization/select-language-culture?view=aspnetcore-9.0) to resolve current culture and IStringLocalizer or Validly's IValidationMessageLocalizer

## Benchmarks

TODO: Finish benchmarks

NOTE: Currently, it's not easy to benchmark it, because benching tools creating request consumes a lot of CPU, much more than the ASP.NET itself. Even using 2 computers - one for ASP.NET, one for benching - is not enough.

Current results (with ASP.NET Core utilizing less than 50 % of CPU):

* Validly: \~55 000 req/sec
* FluentValidation: \~43 000 req/sec
* No validation (just returning Results.Ok()): \~54 000 req/sec - A little bit less than endpoint with Validly validations. Seems like stable result, but I don't rly understand why it is slower.

