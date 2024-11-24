# Manual Validation

<mark style="color:purple;">**Validly**</mark> offers a versatile toolkit for validating your .NET models. You can utilize built-in validation attributes, define custom validation attributes, or implement manual validation logic directly within your model to handle more complex scenarios. Below is an overview of the manual validation options available in <mark style="color:purple;">**Validly**</mark>:

### Custom Validation via `[CustomValidation]`

For scenarios where more flexibility is required, you can use the `[CustomValidation]` attribute. This allows you to write custom logic for validating specific properties. <mark style="color:purple;">**Validly**</mark> will generate an interface for the associated validation method, which you can implement as needed. You have full control over the method's signature and return type, supporting sync and async validations.

Dive deeper into property-level custom validation on the [CustomValidation Attribute](customvalidation-attribute.md) page.

### `BeforeValidate` and `AfterValidate` Hooks

To customize validation behavior at a higher level, you can implement the `BeforeValidate` and `AfterValidate` methods in your objects. These methods allow you to hook into the validation process:

* **BeforeValidate**: Runs before validation starts, letting you perform pre-validation logic or return an early `ValidationResult` to stop further validation.
* **AfterValidate**: Allows you to manipulate or extend the result after validation completes, making it ideal for adding global validation messages or combining results.

Both methods optionally accept a `ValidationContext` parameter, which is useful for scenarios where you need access to parent/root object. You can also use method parameters for dependency injection, allowing you to retrieve services directly from the service provider.

Learn more about how to use these methods on the [Before and After Hooks](before-and-after-hooks.md) page.
