---
icon: hand-wave
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Introduction

<mark style="color:purple;">**Validly**</mark> is a powerful, efficient, and highly customizable validation library for .NET. It leveraging the capabilities of C# Source Generators to produce compile-time validation logic, eliminating runtime overhead. Designed to streamline model validation, Validly automatically generates validation code from attributes and custom rules, simplifying development and improving code maintainability.

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Getting Started</strong></td><td>Quickstart with the <mark style="color:purple;"><strong>Validly</strong></mark></td><td></td><td></td><td><a href="getting-started/quickstart.md">quickstart.md</a></td></tr><tr><td>Installation</td><td>How to install <mark style="color:purple;"><strong>Validly</strong></mark></td><td></td><td></td><td><a href="getting-started/installation.md">installation.md</a></td></tr><tr><td><strong>Basics</strong></td><td>Learn the basics</td><td></td><td></td><td><a href="basics/handling-validation-result.md">handling-validation-result.md</a></td></tr><tr><td>Validators</td><td>Learn about validators</td><td></td><td></td><td><a href="broken-reference">Broken link</a></td></tr></tbody></table>

## Key Features

#### **Compile-Time Code Generation**

Uses C# Source Generators to create validation code at compile-time, eliminating the need for runtime reflection and improving performance.&#x20;

#### **Attribute-Based Validation**

Define validation rules using simple attributes directly on your models, allowing clear and maintainable validation rules.

#### **Property and Object-Level Validation**

Supports validation of individual properties as well as the model as a whole, enabling both fine-grained and aggregate validations.

#### Automatically Added Validators

Options to automatically add validators, like AutoRequire and AutoInEnum, simplify the validation process by automatically applying commonly needed rules based on the data type or structure of your properties.

#### **Customizable Validation Logic**

Extend the library with custom validation attributes and rules to meet unique validation requirements.

#### **Detailed Validation Results**

Provides rich validation results, including per-property error messages and model-wide validation summaries.

#### No Strict Interfaces

Instead of enforcing specific parameter types or method signatures of custom validations, <mark style="color:purple;">**Validly**</mark> identifies validation methods based on their names, enabling greater flexibility in implementation.&#x20;

Custom validation methods can return a single validation message or a collection of them. It can be synchronous or return Task, ValueTask or IAsyncEnumerable for **asynchronous validations**. It can also be void, focusing solely on side effects or performing other operations.

#### **Seamless Integration**

Designed to work smoothly in .NET applications, with support for **dependency injection** and easy configuration.

## Why <mark style="color:purple;">Validly</mark>? Why Attribute-Based Validation?

<mark style="color:purple;">**Validly**</mark> was born out of the need for a simple, performant way to handle validations, particularly when following Domain-Driven Design (DDD). In DDD, entities are responsible for their own validation. While validations on the API level are important, they cannot be the sole safeguard. The domain must validate entities independently, as the API is just one entry point to your system. Other sources, like background jobs or message queues, can also create or interact with domain objects.

Humans make mistakes, and developers are no exception. Relying solely on API-level validations is risky; you need a robust validation layer directly in your domain to ensure data integrity across all interactions.

### **Why Not Existing Libraries?**

Libraries like FluentValidation are powerful, but they have limitations:

* Reflection-based design: While flexible, this approach bypasses static code analysis, making your code harder to refactor and less performant.
* Complexity: These libraries often require additional boilerplate code and are more suited to abstract validation pipelines, such as middleware in an API, than to domain entities.

<mark style="color:purple;">**Validly**</mark> solves these issues by offering an attribute-based, source-generator-powered approach for validations. It combines simplicity, static analysis support, and high performance, making it an ideal choice for both API-level and domain-level validation.

### **Why Attribute-Based Validation?**

Most validations are straightforward and can be expressed cleanly with attributes. For example, validating that a string is not empty or a number falls within a range shouldn’t require excessive boilerplate. Attributes allow you to express such requirements concisely and directly within your model.

Separating validations from the model may even be considered an anti-pattern or a violation of the Single Responsibility Principle. When validations are defined externally, it increases the likelihood of developer errors—such as forgetting to update validations when the model changes. By keeping validations close to the model, <mark style="color:purple;">**Validly**</mark> ensures consistency, simplifies maintenance, and minimizes mistakes.

## Performance

Validly is one of the fastest and most memory-optimized validation libraries for .NET. Built without reliance on reflection, it delivers pure, highly optimized C# code for exceptional performance. By leveraging memory pooling, Validly ensures zero memory allocation on the hot path, making it ideal for high-throughput, performance-critical applications.

Check out [Benchmarks ](getting-started/benchmarks.md)for more information.

