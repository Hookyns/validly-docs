---
icon: earth-europe
---

# Localization

<mark style="color:purple;">**Validly**</mark> is designed with localization in mind from the ground up. Validation errors are represented using the `ValidationMessage` class, which includes the following properties:

* **Message**: The default error text.
* **ResourceKey**: A localization key that allows the message to be translated.
* **Args**: An optional array of parameters that can be used for formatting or other purposes.

This design makes it straightforward to integrate localized validation errors into your application.

## API-Ready Validation Results

The `ValidationResult` is crafted to be API-friendly. It can be sent directly to the front end, enabling localization to occur on the client side rather than the back end (though the back end can handle localization if desired). If a translation for the `ResourceKey` is unavailable on the client, the fallback is to use the default `Message` text.
