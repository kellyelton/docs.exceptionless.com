---
layout: docs
edit_path: troubleshooting
title: Troubleshooting
prev_section: security
next_section: faq
permalink: /contents/troubleshooting/
---

If your events aren't being sent to the server there are a few things that you can try to diagnose the issue.

## Update your client

Please make sure that you are using the [latest version of the client](/contents/upgrading).

## Ensure that the queue has time to process

If you are using Exceptionless in a scenario where an event is submitted and the process is immediately terminated, then you will need to make sure that the queue is processed before the application ends. Please note that this will happen automatically if you are not using the `Exceptionless.Portable` package. 

Events are queued to disk and sent in the background, if the application isn't running then the events cannot be sent. You can manually force the queue to be processed by calling the following line of code before before the process ends:

{% highlight c# %}
ExceptionlessClient.Default.ProcessQueue();
{% endhighlight %}

This will cause the event queue to be processed synchronously and the events to be reported. If this doesn't
solve the issue then please enable client logging and contacting us the log file.

## How to locate the default isolated storage queue folder

By default, Exceptionless stores errors in an isolated storage folder. You can find this folder using the 1st 8
characters of your API key. So if your API key is `a7aa250fce7e4e36a22a7031cf2337c8`, then you would search in
the `C:\ProgramData\IsolatedStorage` folder for a folder named `a7aa250f`.

## Firewall / Proxy
If you are behind a proxy or firewall, please ensure that you can connect to [https://collector.exceptionless.io](https://collector.exceptionless.io)

Your proxy settings should be picked up automatically by the Exceptionless client, but you can also try manually configuring the settings by adding a section to your app/web.config file. 

**NOTE: Some clients may not support proxies. Proxies are not supported in Portable Class Libraries (PCL). If you are only using the `Exceptionless` portable class library package, then proxies will not work.** 

{% highlight xml %}
<system.net>
    <defaultProxy useDefaultCredentials="true">
      <proxy proxyaddress="proxyAddress" usesystemdefault="true"/>
    </defaultProxy>
</system.net>
{% endhighlight %}

## Enable client logging

The Exceptionless client can be configured to write diagnostic messages to a log file to 
help diagnose any issues with the client. You can enable logging via configuration using one of the following
methods:

*Make sure you have write access to the file you specify for the log path.*

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY" enableLogging="true" logPath="C:\exceptionless.log" />
{% endhighlight %}

### Code
{% highlight c# %}
ExceptionlessClient.Default.Configuration.UseFileLogger("C:\\exceptionless.log");
{% endhighlight %}

## Debugging the source code
You can also debug the Exceptionless NuGet packages by configuring the Visual Studio source server integration. Please follow the [Symbol Source documentation](http://www.symbolsource.org/Public/Home/VisualStudio) on configuring Visual Studio.
