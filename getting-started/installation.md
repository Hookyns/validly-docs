---
icon: cube
---

# Installation

## Prerequisites <a href="#prerequisites" id="prerequisites"></a>

* A project targeting .NET compatible with netstandard 2.0,
  * [Here](https://learn.microsoft.com/en-us/dotnet/standard/net-standard?tabs=net-standard-2-0#select-net-standard-version) is a table with supported implementations.

## Installation

{% tabs %}
{% tab title=".NET CLI" %}
**Core package**

```sh
dotnet add package Validly
```

**Set of predefined validators**

```sh
dotnet add package Validly.Extensions.Validators
```

**Source Generator**

```sh
dotnet add package Validly.SourceGenerator
```
{% endtab %}

{% tab title="Package Manager Console" %}
**Core package**

```sh
Install-Package Validly
```

**Set of predefined validators**

```sh
Install-Package Validly.Extensions.Validators
```

Source Generator

```sh
Install-Package Validly.SourceGenerator
```
{% endtab %}

{% tab title="PackageReference" %}
**Core package**

```xml
<PackageReference Include="Validly" Version="1.0.0" />
```

**Set of predefined validators**

```xml
<PackageReference Include="Validly.Extensions.Validators" Version="1.0.0" />
```

Source Generator

```xml
<PackageReference Include="Validly.SourceGenerator" Version="1.0.0" />
```
{% endtab %}
{% endtabs %}

## .NET Framework

To use this library with .NET Framework, there are some dependencies you may need to install:

* `System.Threading.Tasks.Extensions`
* `Microsoft.Extensions.DependencyInjection`
* `Microsoft.Bcl.AsyncInterfaces`

These packages can be installed using a NuGet package manager, or the dotnet CLI:

<pre class="language-shell"><code class="lang-shell">dotnet add package System.Threading.Tasks.Extensions
<strong>dotnet add package Microsoft.Extensions.DependencyInjection
</strong>dotnet add package Microsoft.Bcl.AsyncInterfaces
</code></pre>

