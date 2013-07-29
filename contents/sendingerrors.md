---
layout: docs
title: Sending Errors
prev_section: configuration
next_section: troubleshooting
permalink: /contents/sendingerrors/
---

In addition to automatically sending all unhandled exceptions, you may want to manually send exceptions to the service.
You can do so using code like this:

{% highlight c# %}
try {
    throw new ApplicationException(Guid.NewGuid().ToString());
} catch (Exception ex) {
    ex.ToExceptionless().MarkAsCritical().Submit();
}
{% endhighlight %}
