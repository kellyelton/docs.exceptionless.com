---
layout: docs
edit_path: sendingevents
title: Sending Events
prev_section: configuration
next_section: search
permalink: /contents/sendingevents/
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
        .SetUserIdentity(user.EmailAddress)
        .Submit();
}
{% endhighlight %}

## Modifying Unhandled Exception Reports

You can get notified, add additional information or ignore unhandled exceptions by wiring up to the
`SubmittingEvent` event.

{% highlight c# %}
// Wire up to this event in somewhere in your application's startup code.
ExceptionlessClient.Default.SubmittingEvent += OnSubmittingEvent;

void OnSubmittingEvent(object sender, EventSubmittingEventArgs e) {
    // Only handle unhandled exceptions.
    if (!e.IsUnhandledError)
        return;

    // Ignore 404s
    if (e.Event.IsNotFound()) {
        e.Cancel = true;
        return;
    }

    // Get the error object.
    var error = e.Event.GetError();
    if (error == null)
        return;

    // Ignore 401 (Unauthorized) and request validation errors.
    if (error.Code == "401" || error.Type == "System.Web.HttpRequestValidationException") {
        e.Cancel = true;
        return;
    }
    
    // Add some additional data to the report.
    e.Event.AddObject(order, "Order", excludedPropertyNames: new [] { "CreditCardNumber" }, maxDepth: 2);
    e.Event.Tags.Add("Order");
    e.Event.MarkAsCritical();
    e.Event.SetUserIdentity(user.EmailAddress);
}
{% endhighlight %}
