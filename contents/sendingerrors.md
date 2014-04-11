---
layout: docs
edit_path: sendingerrors
title: Sending Errors
prev_section: configuration
next_section: security
permalink: /contents/sendingerrors/
---

Once configured, Exceptionless will automatically send any unhandled exceptions that happen in your application.

## Manually Sending Errors

In addition to automatically sending all unhandled exceptions, you may want to manually send exceptions to the service.
You can do so by importing the Exceptionless namespace and using code like this:

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

## Modifying Unhandled Exception Reports

You can get notified, add additional information or ignore unhandled exceptions by wiring up to the
`UnhandledExceptionReporting` event.

{% highlight c# %}
// Wire up to this event in somewhere in your application's startup code.
ExceptionlessClient.Current.UnhandledExceptionReporting += OnUnhandledExceptionReporting;

void OnUnhandledExceptionReporting(object sender, UnhandledExceptionReportingEventArgs args) {
    // ignore 404 and request validation errors
    if (args.Error.Code == "404" || args.Error.Type == "System.Web.HttpRequestValidationException")
        args.Cancel = true;
        return;
    }
    
    // add some additional data to the report
    args.Error.AddObject(order, "Order", excludedPropertyNames: new [] { "CreditCardNumber" }, maxDepth: 2);
    args.Error.Tags.Add("Order");
    args.Error.MarkAsCritical();
    args.Error.UserEmail = user.EmailAddress;
}
{% endhighlight %}

