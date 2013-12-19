---
layout: docs
edit_path: troubleshooting
title: Troubleshooting
prev_section: sendingerrors
next_section: faq
permalink: /contents/troubleshooting/
---

If your errors aren't being sent to the server there are a few things that you can try to diagnose the issue.

## Update your client

Please make sure that you are using the latest version of the client.

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

## Enable client logging

The Exceptionless client can be configured to write diagnostic messages to a log file to 
help diagnose any issues with the client. You can enable logging via configuration using one of the following
methods:

### Configuration file

{% highlight xml %}
<exceptionless apiKey="YOUR_API_KEY" enableLogging="true" logPath="C:\exceptionless.log" />
{% endhighlight %}

### Attribute

{% highlight c# %}
[assembly: Exceptionless("YOUR_API_KEY", EnableLogging = true, LogPath = "C:\\exceptionless.log")]
{% endhighlight %}

*Make sure you have write access to the file you specify for the log path.*

### Integrate the Exceptionless logs with your own logging mechanism

You can simply create a class that implements the `IExceptionlessLog` interface and then assign your implementation
using `ExceptionlessClient.Current.Log = yourLogImpl;`.

Here is a sample implementation that redirects the log messages to NLog:

{% highlight c# %}
public class NLogExceptionlessLog : IExceptionlessLog {
    public void Error(string message, string source = null, Exception exception = null) {
        Log.Error().LoggerName(source).Exception(exception).Message(message).Write();
    }

    public void Info(string message, string source = null) {
        Log.Info().LoggerName(source).Message(message).Write();
    }

    public void Debug(string message, string source = null) {
        if (Debugger.IsAttached)
            Log.Debug().LoggerName(source).Message(message).Write();
    }

    public void Warn(string message, string source = null) {
        Log.Warn().LoggerName(source).Message(message).Write();
    }

    public void Trace(string message, string source = null) {
        Log.Trace().LoggerName(source).Message(message).Write();
    }

    public void Flush() {}
}
{% endhighlight %}

## How to locate the default isolated storage queue folder

By default, Exceptionless stores errors in an isolated storage folder. You can find this folder using the 1st 8
characters of your API key. So if your API key is `a7aa250fce7e4e36a22a7031cf2337c8`, then you would search in
the `C:\ProgramData\IsolatedStorage` folder for a folder named `a7aa250f`.

## Firewall
If you are behind a proxy or firewall, please ensure that you can connect to [https://collector.exceptionless.com](https://collector.exceptionless.com)
