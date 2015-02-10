---
layout: docs
edit_path: upgrading
title: Upgrading the Exceptionless client
prev_section: faq
permalink: /contents/upgrading/
---

##Upgrading from all previous versions of Exceptionless
Please read this guide when upgrading from any version of Exceptionless.

1. Open the NuGet Package Manager dialog.
2. Click on the Updates tab.
3. *NOTE: To upgrade to 2.x preview you will have to select "Include Prerelease" from the dropdown.*
4. Select the exceptionless nuget packages and click the Update button.

For more information please see the official [NuGet documentation](https://docs.nuget.org/consume/Package-Manager-Dialog).

##Upgrading from Exceptionless 1.x

Please read this guide when upgrading from Exceptionless 1.x. The Exceptionless latest client has a few breaking changes from 1.x client that users users should be aware of when upgrading. Please follow the guide below after upgrading your NuGet packages from version 1.x to the latest version.

### ExceptionlessClient API changes

#### Methods
1. `ExceptionlessClient.Current.GetLastErrorId()` has been renamed to `ExceptionlessClient.Default.GetLastReferenceId()`. *NOTE: To have a reference id automatically generated, you must call `ExceptionlessClient.Default.Configuration.UseReferenceIds()`*

#### Properties
1. `ExceptionlessClient.Current` has been deprecated and replaced with `ExceptionlessClient.Default`.
2. `ErrorBuilder` has been renamed to `EventBuilder`.

#### Events
1. `event EventHandler<SendErrorCompletedEventArgs> SendErrorCompleted` has been removed. To get notified of when an event has been submitted you must implement a custom `ISubmissionClient` and register it with the dependency resolver (Ex. `client.Configuration.Resolver.Register<ISubmissionClient, SubmissionClient>()` ).
2. `event EventHandler<RequestSendingEventArgs> RequestSending` has been removed. To override how an event is sent you must implement a custom `ISubmissionClient` and register it with the dependency resolver (Ex. `client.Configuration.Resolver.Register<ISubmissionClient, SubmissionClient>()` ).
3. `event EventHandler<UnhandledExceptionReportingEventArgs> UnhandledExceptionReporting` has been removed and replaced with `event EventHandler<EventSubmittingEventArgs> SubmittingEvent`. You'll need to wire up to `SubmittingEvent` and check the `IsUnhandledError` property. *NOTE: Error has been renamed to Event on the Event Args class.*

##### Overview
{% highlight c# %} 
ExceptionlessClient.Default.SubmittingEvent += OnSubmittingEvent;

private static void OnSubmittingEvent(object sender, EventSubmittingEventArgs e) {
  if (!e.IsUnhandledError)
    return;
}
{% endhighlight %} 

### Xml configuration changes
**These changes will be automatically upgraded by our NuGet installer.**

1. `queuePath` has been renamed to `storagePath` 
2. `extendedData` has been renamed to `data`.

##### Overview
  {% highlight xml %}
  <exceptionless apiKey="YOUR_API_KEY_HERE" storagePath="|DataDirectory|\Queue">
    <data>
      <add name="SimpleValueFromConfig" value="Exceptionless"/>
    </data>
  </exceptionless>
  {% endhighlight %}

### Attribute configuration changes
1. `QueuePath` has been renamed to `StoragePath`.
2. `ExceptionlessAttribute(string serverUrl, string apiKey, ...)` signature has been changed to `ExceptionlessAttribute(string apiKey)`. The new signature uses object initializers.
 
##### Overview
{% highlight c# %}
[assembly: Exceptionless("YOUR_API_KEY_HERE", ServerUrl = "...", StoragePath = "|DataDirectory|\Queue")]
{% endhighlight %}

*Please contact support for assistance on updating any undocumented upgrade changes.*
