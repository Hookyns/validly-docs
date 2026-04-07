---
icon: microchip
---

# Native AOT

<mark style="color:purple;">Validly</mark> is fully compatible with .NET’s native AOT (Ahead-of-Time) compilation.\
Because it relies on source generation instead of reflection, all validation logic is compiled into your application at build time, making it perfectly suited for AOT scenarios where reflection-based libraries often fail.

While AOT builds typically start faster and consume less memory, they can’t take advantage of JIT’s runtime optimizations. As a result, <mark style="color:purple;">Validly</mark> performs roughly **60% slower under AOT** compared to JIT, which is an expected trade-off for the improved startup performance and deterministic behavior that AOT provides. This performance gap may decrease in the future as Microsoft continues to improve the .NET AOT compiler and its optimization capabilities.

### Performance Tips

*   Setting the `OptimizationPreference` MSBuild property to `Speed` instructs the publishing process to favor code execution speed.<br>

    ```xml
    <OptimizationPreference>Speed</OptimizationPreference>
    ```
* Make your custom validators and validatable objects `sealed`.
