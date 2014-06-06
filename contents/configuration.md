---
layout: docs
edit_path: configuration
title: Configuration
prev_section: gettingstarted
next_section: sendingerrors
permalink: /contents/configuration/
---

Exceptionless can be configured in multiple ways.

## Config File

Exceptionless can be configured using a config section in your web.config or app.config depending on what kind of
project you have. Installing the correct NuGet package should automatically add the necessary configuration
elements.  It should look like this:

{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <configSections>
    <section name="exceptionless" type="Exceptionless.Configuration.ExceptionlessSection, Exceptionless" requirePermission="false" />
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

## Attribute

You can also configure Exceptionless using attributes like this:

{% highlight c# %}
[assembly: Exceptionless("YOUR_API_KEY")]
{% endhighlight %}

## Using a Custom Error Queue Folder

By default the Exceptionless client stores errors in an isolated storage folder. If you want to change it to use a
different folder, then you can use the `QueuePath` setting. If you specify a `QueuePath`, make sure that whatever
identity the application is running under has full permissions to that folder.

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY" queuePath="C:\ExceptionlessErrors" />
{% endhighlight %}

### Attribute

{% highlight c# %}
[assembly: Exceptionless("YOUR_API_KEY", QueuePath="C:\\ExceptionlessErrors")]
{% endhighlight %}


## WCF Configuration

You can also configure exceptionless to capture all WCF exceptions following the steps below.
1. Install the [Exceptionless.Web](http://www.nuget.org/packages/Exceptionless.Web/) NuGet package. 
2. Configure your Api Key (see the previous section).
3. Add the ExceptionlessWcfHandleErrorAttribute to your WCF Classes.

{% highlight c# %}
[ExceptionlessWcfHandleErrorAttribute]
{% endhighlight %}


## Disabling Exceptionless during testing

You can disable Exceptionless from reporting errors during testing using the `Enabled` setting.

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY" enabled="false" />
{% endhighlight %}

### Attribute

{% highlight c# %}
[assembly: Exceptionless("YOUR_API_KEY", Enabled=false)]
{% endhighlight %}

## Custom config settings

Exceptionless allows you to add custom config values to your Exceptionless clients that can be set through the client config section, attributes or remotely on the project settings. These config values can be accessed and used within your app to control things like wether or not to send custom data with your reports. For example, you could have a `IncludeOrderData` flag in your config that you use to control wether or not you add a custom order object to your Exceptionless report data. You can even remotely turn the setting on or off from your project settings. Here is an example of doing that:

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY">
  <settings>
    <add name="IncludeOrderData" value="true" />
  </settings>
</exceptionless>
{% endhighlight %}

Or in a config attribute like:
{% highlight c# %}
[assembly: ExceptionlessSetting("IncludeOrderData", "true")]
{% endhighlight %}

Then in your app, you can check the setting and determine if you should include the order data or not:

{% highlight c# %}
try {
  ...
} catch (Exception ex) {
  var report = ex.ToExceptionless();
  if (ExceptionlessClient.Current.Configuration["Blah"] == "true")
      report.AddObject(order);
  report.Submit();
}
{% endhighlight %}

## Enabling trace message collection

One config setting built into Exceptionless can be used to include the last X trace log messages with your error reports. You can enable this setting by specifying a `TraceLogLimit` setting with a value greater than 0. This value is the maxiumum number of trace messages that will be submitted with the error report.
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
[assembly: ExceptionlessSetting(ClientConfiguration.TraceLogLimitKey, "10")]
{% endhighlight %}

## Adding static extended data values with every report

You can have the Exceptionless client automatically add extended data values to every report that it submits like this:

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY">
    <extendedData>
      <add name="Data1" value="Exceptionless"/>
      <add name="Data2" value="10"/>
      <add name="Data3" value="true"/>
      <add name="Data4" value="{ 'Property1': 'Exceptionless', 'Property2: 10, 'Property3': true }"/>
    </extendedData>
</exceptionless>
{% endhighlight %}

## Adding custom tags with every report

You can have the Exceptionless client automatically add specific tags to every report that it submits like this:

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY" tags="Tag1,Tag2" />
{% endhighlight %}


## Self hosted options
The Exceptionless client can also be configured to send data to your self hosted instance. This is configured by setting the `serverUrl` setting to point to your exceptionless instance. Please note that if you do not have SSL configured you
must set the `enableSSL` setting to `false`.

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY" serverUrl="http://localhost" enableSSL="false" />
{% endhighlight %}

### Attribute

{% highlight c# %}
[assembly: Exceptionless("YOUR_API_KEY", ServerUrl = "http://localhost", EnableSSL = false)]
{% endhighlight %}
