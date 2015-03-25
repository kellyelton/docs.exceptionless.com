---
layout: docs
edit_path: sendingevents
title: Sending Events
prev_section: configuration
next_section: search
permalink: /contents/sendingevents/
---

Once configured, Exceptionless will automatically send any unhandled exceptions that happen in your application. The sections below will show you how to send us different event types as well as customize the data that is sent in.

## Sending Events

You may also want to send us log messages, feature usages or other kinds of events. You can do this very easily with our fluent api.

{% highlight c# %}
// Submit logs
ExceptionlessClient.Default.SubmitLog("Logging made easy");
ExceptionlessClient.Default.SubmitLog(typeof(Program).FullName, "This is so easy", "Info");
ExceptionlessClient.Default.CreateLog("Logging made easy").AddTags("Exceptionless").Submit();

// Submit feature usages
ExceptionlessClient.Default.SubmitFeatureUsage("MyFeature");
ExceptionlessClient.Default.CreateFeatureUsage("MyFeature").AddTags("Exceptionless").Submit();

// Submit a 404
ExceptionlessClient.Default.SubmitNotFound("/somepage");
ExceptionlessClient.Default.CreateNotFound("/somepage").AddTags("Exceptionless").Submit();

// Submit a custom event type
ExceptionlessClient.Default.SubmitEvent(new Event { Message = "Low Fuel", Type = "racecar", Source = "Fuel System" });
{% endhighlight %}

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

You can easily include additional information in your error reports using our fluent event builder API.

{% highlight c# %}
try {
    throw new ApplicationException("Unable to create order from quote.");
} catch (Exception ex) {
    ex.ToExceptionless()
        // Set the reference id of the event so we can search for it later (reference:id).
        // This will automatically be populated if you call ExceptionlessClient.Default.Configuration.UseReferenceIds();
        .SetReferenceId(Guid.NewGuid().ToString("N"))
        // Add the order object but exclude the credit number property.
        .AddObject(order, "Order", excludedPropertyNames: new [] { "CreditCardNumber" }, maxDepth: 2)
        // Set the quote number.
        .SetProperty("Quote", 123)
        // Add an order tag.
        .AddTags("Order")
        // Mark critical.
        .MarkAsCritical()
        // Set the coordinates of the end user.
        .SetGeo(43.595089, -88.444602)
        // Set the user id that is in our system and provide a friendly name.
        .SetUserIdentity(user.Id, user.FullName)
        // Set the users description of the error.
        .SetUserDescription(user.EmailAddress, "I tried creating an order from my saved quote.")
        // Submit the event.
        .Submit();
}
{% endhighlight %}

## Modifying Unhandled Exception Reports

You can get notified, add additional information or ignore unhandled exceptions by wiring up to the
`SubmittingEvent` event.

{% highlight c# %}
// Wire up to this event in somewhere in your application's startup code.
ExceptionlessClient.Default.SubmittingEvent += OnSubmittingEvent;

private void OnSubmittingEvent(object sender, EventSubmittingEventArgs e) {
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
    
    // Ignore any exceptions that were not thrown by our code.
    var handledNamespaces = new List<string> { "Exceptionless" };
    if (!error.StackTrace.Select(s => s.DeclaringNamespace).Distinct().Any(ns => _handledNamespaces.Any(ns.Contains))) {
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
