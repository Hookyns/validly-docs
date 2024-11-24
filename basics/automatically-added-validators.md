---
description: >-
  Automatically added validators, like AutoRequire and AutoInEnum, simplify the
  validation process by automatically applying commonly needed rules based on
  the data type or structure of your properties.
icon: wand-sparkles
---

# Automatically Added Validators

## Required

When the [AutoRequire](../getting-started/configuration.md#autorequire) option is enabled, <mark style="color:purple;">**Validly**</mark> automatically adds a `Required` validator to every property of a reference type that is not nullable. This ensures that non-nullable properties are always validated for presence, reducing the need for manual annotations and promoting more concise and reliable validation rules.

## InEnum

When the [AutoInEnum](../getting-started/configuration.md#autoinenum) option is enabled, <mark style="color:purple;">**Validly**</mark> automatically adds a `InEnum` validator to every Enum property. This ensures that the property value is always validated against the defined set of enum members, preventing invalid or undefined values from passing through.

{% hint style="info" %}
We recommend avoiding defining enum members with a value of zero. Without a zero value in the enum, the default value (`0`) automatically signifies an invalid state. This becomes particularly useful in scenarios like API requests. If an enum property receives no value or is null while being non-nullable, the resulting object instance will assign the default value of zero to the property. In such cases, the **InEnum** validator will detect the default value as invalid, helping to identify missing or incorrect input.&#x20;

However, if zero is assigned to a valid enum member, it becomes impossible to distinguish between a valid value and an unintentional default, potentially leading to undetected bad requests.
{% endhint %}
