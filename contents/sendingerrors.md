---
layout: docs
title: Sending Errors
prev_section: configuration
next_section: troubleshooting
permalink: /contents/sendingerrors/
---

Once configured, Exceptionless will automatically send any unhandled exceptions that happen in your application.

## Manually Sending Errors

In addition to automatically sending all unhandled exceptions, you may want to manually send exceptions to the service.
You can do so using code like this:

{% highlight c# %}
try {
    throw new ApplicationException(Guid.NewGuid().ToString());
} catch (Exception ex) {
    ex.ToExceptionless().Submit();
}
{% endhighlight %}

## Sending Additional Information

You can easily include additional information in your error reports using our fluent error builder API.

{% highlight c# %}
try {
    throw new ApplicationException(Guid.NewGuid().ToString());
} catch (Exception ex) {
    ex.ToExceptionless()
        .AddObject(order, "Order", excludedPropertyNames: new [] { "CreditCardNumber" }, maxDepth: 2)
        .AddTags("Order", "User")
        .MarkAsCritical()
        .SetUserEmail(user.EmailAddress)
        .Submit();
}
{% endhighlight %}
