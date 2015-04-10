---
layout: docs
edit_path: configuration
title: Configuration
prev_section: gettingstarted
next_section: sendingevents
permalink: /contents/configuration/
---

The following sections will walk you through configuring Exceptionless to fit your specific requirements. The sections below assume that you already have an Exceptionless Api Key. You can find your Exceptionless Api Key by [clicking on your project in the project list](https://be.exceptionless.io/project/list). Next, click on the `Api Keys` tab to see your projects Api Keys.

## ExceptionlessClient Configuration

The examples below will show you the various ways (configuration file, attributes or code) the ExceptionlessClient may be configured. Please note that the package (Ex. `Exceptionless.WebApi`) you are using will contain a detailed read me with the best way to configure the ExceptionlessClient for your specific platform.

### Config File

Exceptionless can be configured using a config section in your web.config or app.config depending on what kind of
project you have. Installing the correct NuGet package should automatically add the necessary configuration
elements.  It should look like this:

{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <configSections>
    <section name="exceptionless" type="Exceptionless.ExceptionlessSection, Exceptionless.Extras" />
  </configSections>
  <!-- attribute names are cases sensitive, must specify a path that you have write access to -->
  <exceptionless apiKey="API_KEY_HERE" enableLogging="true" logPath="C:\log.txt" />
  ...
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false" />
    <modules>
      <remove name="ExceptionlessModule" />
      <add name="ExceptionlessModule" type="Exceptionless.Mvc.ExceptionlessModule, Exceptionless.Mvc" />
    </modules>
    ...
  </system.webServer>
</configuration>
{% endhighlight %}

### Attribute

You can also configure Exceptionless using attributes like this:

{% highlight c# %}
using Exceptionless.Configuration;
[assembly: Exceptionless("YOUR_API_KEY")]
{% endhighlight %}

### Code

{% highlight c# %}
using Exceptionless;

var client = new ExceptionlessClient(c => {
    c.ApiKey = "YOUR_API_KEY";
    c.SetVersion(version);
});

// You can also set the api directly on the default instance.
ExceptionlessClient.Default.Configuration.ApiKey = "YOUR_API_KEY"
{% endhighlight %}

## Exceptionless Portable Class Library (PCL) Configuration
If you are using only the `Exceptionless.Portable` package, you'll need to configure exceptionless via attribute config or code. If you choose the attribute method, you'll need to read the configuration on startup.

{% highlight c# %}
using Exceptionless;
ExceptionlessClient.Default.Configuration.ReadFromAttributes(typeof(MyClass).Assembly)
{% endhighlight %}

You will also need to wire up to any error handlers as the `Exceptionless` PCL package doesn't know what platform you are running on. 

It's also worth noting that when using the `Exceptionless` PCL package you will the very basic feature set:

1. Basic stacking of exceptions. PCL libraries don't have access to an errors stack frames so they can't be broken down.
2. Basic `ISubmissionClient` that doesn't support proxies.
3. No Environmental Information will be sent.

For these reasons if you are on a known platform then use the platform specific package to save you time configuring while giving you more contextual information.

## Using a Custom Event Queue Folder

By default the Exceptionless client stores events in an isolated storage folder. If you want to change it to use a
different folder, then you can use the `storagePath` attribute or call `UseFolderStorage`. Please make sure that whatever identity the application is running under has full permissions to that folder.

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY" storagePath="C:\ExceptionlessEvents" />
{% endhighlight %}

### Code

{% highlight c# %}
using Exceptionless;
ExceptionlessClient.Default.Configuration.UseFolderStorage("C:\\ExceptionlessEvents");
{% endhighlight %}

You can also use in memory storage, this is recommended for high throughput logging scenarios. The client will store events in memory instead of serializing the events to disk, but at the expense that any unsubmitted events will be lost on application exit.

{% highlight c# %}
using Exceptionless;
ExceptionlessClient.Default.Configuration.UseInMemoryStorage();
{% endhighlight %}

## WCF Configuration

You can also configure exceptionless to capture all WCF exceptions following the steps below.

1. Install the [Exceptionless.Web](http://www.nuget.org/packages/Exceptionless.Web/) NuGet package. 
2. Configure your Api Key (see the previous section).
3. Add the ExceptionlessWcfHandleErrorAttribute to your WCF Classes.

{% highlight c# %}
[Exceptionless.Web.ExceptionlessWcfHandleErrorAttribute]
{% endhighlight %}


## Disabling Exceptionless during testing

You can disable Exceptionless from reporting events during testing using the `Enabled` setting.

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY" enabled="false" />
{% endhighlight %}

### Attribute

{% highlight c# %}
using Exceptionless.Configuration;
[assembly: Exceptionless("YOUR_API_KEY", Enabled=false)]
{% endhighlight %}

## Custom config settings

Exceptionless allows you to add custom config values to your Exceptionless clients that can be set through the client config section, attributes or remotely on the project settings. These config values can be accessed and used within your app to control things like wether or not to send custom data with your reports. For example, you could have a `IncludeOrderData` flag in your config that you use to control wether or not you add a custom order object to your Exceptionless report data. You can even remotely turn the setting on or off from your project settings. Here is an example of doing that:

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY">
  <settings>
    <add name="IncludeOrderData" value="true" />
  </settings>
</exceptionless>
{% endhighlight %}

### Attribute

{% highlight c# %}
using Exceptionless.Configuration;
[assembly: ExceptionlessSetting("IncludeOrderData", "true")]
{% endhighlight %}

Then in your app, you can check the setting and determine if you should include the order data or not:

{% highlight c# %}
using Exceptionless;

try {
  ...
} catch (Exception ex) {
  var report = ex.ToExceptionless();
  if (ExceptionlessClient.Default.Configuration.Settings["IncludeOrderData"] == "true")
      report.AddObject(order);
  report.Submit();
}
{% endhighlight %}

## Adding static extended data values with every report

You can have the Exceptionless client automatically add extended data values to every report that it submits like this:

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY">
    <data>
      <add name="Data1" value="Exceptionless"/>
      <add name="Data2" value="10"/>
      <add name="Data3" value="true"/>
      <add name="Data4" value="{ 'Property1': 'Exceptionless', 'Property2: 10, 'Property3': true }"/>
    </data>
</exceptionless>
{% endhighlight %}

### Code

{% highlight c# %}
using Exceptionless;
ExceptionlessClient.Default.Configuration.DefaultData["Data1"] = "Exceptionless";
{% endhighlight %}

## Adding custom tags with every report

You can have the Exceptionless client automatically add specific tags to every report that it submits like this:

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY" tags="Tag1,Tag2" />
{% endhighlight %}

### Code

{% highlight c# %}
using Exceptionless;
ExceptionlessClient.Default.Configuration.DefaultTags.Add("Tag1");
{% endhighlight %}

## Enabling trace message collection

**Recommended: You can now submit and search log messages with [Exceptionless](/contents/sendingevents)!**

One config setting built into Exceptionless can be used to include the last X trace log messages with your event reports. You can enable this setting by specifying a `TraceLogLimit` setting with a value greater than 0. This value is the maxiumum number of trace messages that will be submitted with the event report.

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY">
  <settings>
    <add name="TraceLogLimit" value="10" />
  </settings>
</exceptionless>
{% endhighlight %}

### Attribute

{% highlight c# %}
using Exceptionless.Configuration;
[assembly: ExceptionlessSetting("TraceLogLimit", "10")]
{% endhighlight %}

## Self hosted options
The Exceptionless client can also be configured to send data to your self hosted instance. This is configured by setting the `serverUrl` setting to point to your Exceptionless instance. Please note that if you do not have SSL configured you
must set the `enableSSL` setting to `false`.

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY" serverUrl="http://localhost" enableSSL="false" />
{% endhighlight %}

### Attribute

{% highlight c# %}
using Exceptionless.Configuration;
[assembly: Exceptionless("YOUR_API_KEY", ServerUrl = "http://localhost", EnableSSL = false)]
{% endhighlight %}
