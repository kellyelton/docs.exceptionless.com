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
[assembly: Exceptionless("YOUR_API_KEY", Enabled="false")]
{% endhighlight %}

## Enabling trace message collection

An error report may also contain trace messages that were written before the error occurred. You can enable this setting by specifying a `TraceLogLimit` setting with a value greater than 0. This value is the maxiumum number of trace messages that will be submitted with the error report.
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
