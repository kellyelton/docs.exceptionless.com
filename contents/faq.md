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

## Q: Can I reset my error data?
A: You can reset your error data by going into the manage project page and clicking the `Delete All Project Data` button.

## Q: What happens if my internet connection goes down?
A: Exceptionless queues all error submissions to disk and will retry them later.

## Q: How can I disable error reporting during testing?
A: Set the `enabled` attribute to `false` in the `exceptionless` config section.

## Q: Is there a minimum version of .NET you need to be targeting to use the Exceptionless client.
A: Yes, your application needs to be targeting .NET 3.5 or newer.

## Q: Can I use Exceptionless under medium trust?
A: Yes, you will need to set the `requirePermission` attribute to `false` in the `exceptionless` config section. This attribute allows the exceptionless client to read the exceptionless config settings. When you are running in medium trust, unhandled exceptions will not be caught. This means that you must submit exceptions to exceptionless manually. We recommend wiring up to the <a href="http://msdn.microsoft.com/en-us/library/24395wz3(v=vs.100).aspx" target="_blank">global application objects application error handler</a> and [submitting the errors manually]({{ site.url }}/contents/sendingerrors).
