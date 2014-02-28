---
layout: docs
edit_path: faq
title: Frequently Asked Questions
prev_section: troubleshooting
permalink: /contents/faq/
---

Here are some answers to frequently asked questions about the Exceptionless service.

## Q: Will Exceptionless slow my application down?
A: Exceptionless queues all error submissions to disk and then processes them in a background thread. We do
everything we can to make sure that we do not slow your app down or crash your app.

## Q: What will happen if my application throws a bunch of exceptions in a very short amount of time?
A: Exceptionless will intelligently try to ensure that the right amount of data is sent in. First, the client will ensure that the same error occurrence isn't submitted repeatedly by multiple error handlers within a very small window of time (E.G., Two seconds). Finally, in some cases the server logic will step in to remove error occurrences that it feels are spam. For example: Your site might be scanned by a bot and throw a bunch of unique 404 errors. Our system will see all of these within a small window of time submitted by a specific IP address. Once it hits a configurable threshold of error occurrences within a specific amount of time, these error occurrences will be removed from the system.

## Q: Can I reset my error data?
A: You can reset your error data at the project level by going into the manage project page and clicking the `Delete All Project Data` button. You can also reset all error data for a specific error stack by going to the error stack page, clicking the `Options` button and clicking `Reset Stats`.

## Q: What happens if my internet connection goes down?
A: Exceptionless queues all error submissions to disk and will retry them later.

## Q: How can I disable error reporting during testing?
A: Set the `enabled` attribute to `false` in the `exceptionless` config section.

## Q: Can I send log messages along with my error reports?
A: Yes, you can have Exceptionless automatically include the last X trace log messages with each error report using the `TraceLogLimit` config setting like this:

{% highlight xml %}
<exceptionless apiKey="...">
  <settings>
    <add name="TraceLogLimit" value="10" />
  </settings>
</exceptionless>
{% endhighlight %}

## Q: Is there a minimum version of .NET you need to be targeting to use the Exceptionless client.
A: Yes, your application needs to be targeting .NET 3.5 or newer.

## Q: Can I use Exceptionless under medium trust?
A: Yes, you will need to set the `requirePermission` attribute to `false` in the `exceptionless` config section. This attribute allows the exceptionless client to read the exceptionless config settings. When you are running in medium trust, unhandled exceptions will not be caught. This means that you must [submit exceptions]({{ site.url }}/contents/sendingerrors) to Exceptionless manually.

## Q: Can I use my own domain name for reporting errors to exceptionless.com?
A: Yes, you can simply create a [CNAME record](http://en.wikipedia.org/wiki/CNAME_record) that points to `collector.exceptionless.com` and then change the Exceptionless client to use the alias that you created like this:

{% highlight xml %}
<exceptionless apiKey="..." serverUrl="https://exceptionless.mydomain.com" />
{% endhighlight %}
