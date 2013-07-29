---
layout: docs
title: Troubleshooting
prev_section: sendingerrors
permalink: /contents/troubleshooting/
---

If you ever run into problems using Exceptionless, here's a few tips
that will get you up and running. If you are still experiencing issues, 
please don't hesitate to contact us via support.

## Installation Problems

If you encounter errors while installing Exceptionless via NuGet. 
Please [contact us](https://github.com/codesmithtools/docs.exceptionless.com/issues/new) 
with any errors that you are seeing in the NuGet's Package Manager Console.

## Exceptionless Client Logging.

The Exceptionless Client can be configured to write diagnostic messages to an log file to 
help diagnose any issues with the client. You will need to turn on logging via configuration.
First you must turn on Logging by setting EnableLogging to true and specify a LogPath with a 
file path. Please make sure that the current user has read/write file permissions for the 
specified file path.

**If you are experiencing a client issue, please always include a client log when contacting 
support.**

### Attributes

{% highlight c# %}
[assembly: Exceptionless("YOUR_API_KEY", EnableLogging = true, LogPath = "C:\\exceptionless.log")]
{% endhighlight %}

### Configuration File

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY" enableLogging="true" logPath="C:\exceptionless.log" />
{% endhighlight %}


## Help! No errors are being submitted

The following section will help you if are experiencing issues where the Exceptionless client is 
not submitting any errors.

One of the main reasons an error wouldn't be submitted is if the application ended prematurely. 
Errors are queued to disk and sent in the background, if the application isn't running then the 
errors cannot be sent. If you are testing exceptionless in a console application, please make sure
you are calling the following line of code before the application quits:

{% highlight c# %}
ExceptionlessClient.Current.ProcessQueue();
{% endhighlight %}

This will cause the error queue to be processed synchronously and the error to be reported. If this doesn't
solve the issue then please enabling client logging and contacting us the log file.
