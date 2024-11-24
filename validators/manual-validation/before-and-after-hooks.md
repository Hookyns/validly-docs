# Before And After Hooks

For even more control over the validation process, <mark style="color:purple;">**Validly**</mark> allows you to implement the `BeforeValidate` and `AfterValidate` methods within your class.

* **`BeforeValidate`**: Called before the validation process begins, allowing you to perform any pre-validation logic.
* **`AfterValidate`**: Called after the validation completes, allowing you to adjust the final validation result or add global messages.

<pre class="language-csharp"><code class="lang-csharp">[Validatable]
public partial class CreateUserRequest
{
    [Required]
    [MinLength(3)]
    public string Name { get; set; }

    private void BeforeValidate()
<strong>    {
</strong>        // Perform custom logic before validation starts
    }

    private ValidationResult AfterValidate(ValidationResult result)
    {
        // Add global messages or adjust validation result after validation
        return result;
    }
}
</code></pre>

Both methods optionally accept a `ValidationContext` parameter, which is useful for scenarios where you need access to parent/root object. You can also use method parameters for **dependency injection**, allowing you to retrieve services directly from the service provider.

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

