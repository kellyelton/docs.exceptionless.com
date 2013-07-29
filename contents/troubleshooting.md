---
layout: docs
title: Troubleshooting
prev_section: sendingerrors
permalink: /contents/troubleshooting/
---

If your errors aren't being sent to the server there are a few things that you can try to diagnose the issue.

## Enable client logging

The Exceptionless client can be configured to write diagnostic messages to a log file to 
help diagnose any issues with the client. You can enable logging via configuration using one of the following
methods:

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY" enableLogging="true" logPath="C:\exceptionless.log" />
{% endhighlight %}

### Attributes

{% highlight c# %}
[assembly: Exceptionless("YOUR_API_KEY", EnableLogging = true, LogPath = "C:\\exceptionless.log")]
{% endhighlight %}

*Make sure you have write access to the file you specify for the log path.*

## Ensure that the queue has time to process

If you are using Exceptionless in a console application or any other scenario where an error is submitted
and the process is immediately terminated, then you will need to make sure that the queue is processed before
the application ends. Errors are queued to disk and sent in the background, if the application isn't running then the 
errors cannot be sent. You can manually force the queue to be processed by calling the following line of code before
before the process ends:

{% highlight c# %}
ExceptionlessClient.Current.ProcessQueue()
{% endhighlight %}

This will cause the error queue to be processed synchronously and the error to be reported. If this doesn't
solve the issue then please enable client logging and contacting us the log file.
