---
layout: docs
edit_path: upgrading
title: Upgrading the Exceptionless client
prev_section: faq
permalink: /contents/upgrading/
---

##Upgrading from all previous versions of Exceptionless
Please read this guide when upgrading from any version of Exceptionless. Upgrading is meant to be an easy process. **Most users will just have to upgrade the NuGet package.** If you run into any issues after upgrading the NuGet packages please take a look at the sections below.

1. Open the NuGet Package Manager dialog.
2. Click on the Updates tab.
3. Select the exceptionless nuget packages and click the Update button.

For more information please see the official [NuGet documentation](https://docs.nuget.org/consume/Package-Manager-Dialog).

##Upgrading from Exceptionless 1.x

Please read this guide when upgrading from Exceptionless 1.x. The Exceptionless latest client has a few breaking changes from 1.x client that users should be aware of when upgrading. Please follow the guide below after upgrading your NuGet packages from version 1.x to the latest version.

### Console and Service users
We've created a new NuGet package [Exceptionless.Console](https://www.nuget.org/packages/exceptionless.console) that should be used in these scenarios.

### ExceptionlessClient API changes

#### Methods
1. `ExceptionlessClient.Current.GetLastErrorId()` has been renamed to `ExceptionlessClient.Default.GetLastReferenceId()`. *NOTE: To have a reference id automatically generated, you must call `ExceptionlessClient.Default.Configuration.UseReferenceIds()`*

##### Advanced
The following changes affect a very small portion of users.

1. `client.Create(Exception)` has been renamed to `client.CreateEvent()`.
2. `client.CreateError(Exception)` has been renamed to `client.CreateException(Exception)`. *NOTE: This now submits the exception.*
3. `client.SubmitError(Error)` has been renamed to `client.SubmitEvent(Event)`.
4. `client.SubmitError(Exception)` and `client.Submit(Exception)` has been renamed to `client.SubmitException(Exception)`.
5. `client.ProcessUnhandledException(Exception)` has been renamed to `client.SubmitUnhandledException(Exception)`.
6. `client.SubmitPatch(string id, object patch)` has been removed.
7. `client.SuspendProcessing()` has been moved to `client.Configuration.Resolver.GetEventQueue().SuspendProcessing()`.
7. `client.UpdateConfiguration()` has been moved to `Exceptionless.Configuration.SettingsManager.UpdateSettings(client.Configuration)`.

#### Properties
1. `ExceptionlessClient.Current` has been deprecated and replaced with `ExceptionlessClient.Default`.

##### Advanced
The following changes affect a very small portion of users.

1. `ErrorBuilder` has been renamed to `EventBuilder`.
2. `client.Tags` has been moved to `client.Configuration.DefaultTags`.
3. `IExceptionlessPlugin` has been replaced with `IEventEnrichment`. *NOTE: Enrichments can be registered via  `client.Configuration.AddEnrichment<IEventEnrichment>();`*
4. `client.Configuration["MySetting"]` has been moved to `client.Configuration.Settings["MySetting"]`.

#### Events
1. `event EventHandler<UnhandledExceptionReportingEventArgs> UnhandledExceptionReporting` has been removed and replaced with `event EventHandler<EventSubmittingEventArgs> SubmittingEvent`. You'll need to wire up to `SubmittingEvent` and check the `IsUnhandledError` property.

##### Advanced
The following changes affect a very small portion of users.

1. `event EventHandler<SendErrorCompletedEventArgs> SendErrorCompleted` has been removed. To get notified of when an event has been submitted you must implement a custom `ISubmissionClient` and register it with the dependency resolver (Ex. `client.Configuration.Resolver.Register<ISubmissionClient, SubmissionClient>()` ).
2. `event EventHandler<RequestSendingEventArgs> RequestSending` has been removed. To override how an event is sent you must implement a custom `ISubmissionClient` and register it with the dependency resolver (Ex. `client.Configuration.Resolver.Register<ISubmissionClient, SubmissionClient>()` ).

##### Overview
{% highlight c# %} 
ExceptionlessClient.Default.SubmittingEvent += OnSubmittingEvent;
...
private static void OnSubmittingEvent(object sender, EventSubmittingEventArgs e) {
  if (!e.IsUnhandledError)
    return;

  if (e.Event.Message == "Important Exception")
    e.Event.Tags.Add("Important");
}
{% endhighlight %} 

### Attribute configuration changes
1. `QueuePath` has been renamed to `StoragePath`.
2. `ExceptionlessAttribute(string serverUrl, string apiKey, ...)` signature has been changed to `ExceptionlessAttribute(string apiKey)`.
 
##### Overview
{% highlight c# %}
[assembly: Exceptionless("YOUR_API_KEY_HERE", ServerUrl = "...", StoragePath = "|DataDirectory|\Queue")]
{% endhighlight %}

### Xml configuration changes
**These changes will be automatically upgraded by our NuGet installer.**

1. `queuePath` has been renamed to `storagePath` 
2. `extendedData` has been renamed to `data`.
3. The `exceptionless` configuration section has been moved into the `Exceptionless.Extras` assembly. *NOTE: Xml configuration is not available if you are only using the PCL client.*

##### Overview
{% highlight xml %}
<configSections>
  <section name="exceptionless" type="Exceptionless.ExceptionlessSection, Exceptionless.Extras"/>
</configSections>

<exceptionless apiKey="YOUR_API_KEY_HERE" storagePath="|DataDirectory|\Queue">
  <data>
    <add name="SimpleValueFromConfig" value="Exceptionless"/>
  </data>
</exceptionless>
{% endhighlight %}

*Please [contact support](https://github.com/exceptionless/Exceptionless/issues/new) for assistance on updating any undocumented upgrade changes.*
