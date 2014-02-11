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
A: You can reset your error data at the project level by going into the manage project page and clicking the `Delete All Project Data` button. You can also reset all error data for a specific error stack by going to the error stack page, clicking the `Options` button and clicking `Reset Stats`.

## Q: What happens if my internet connection goes down?
A: Exceptionless queues all error submissions to disk and will retry them later.

## Q: How can I disable error reporting during testing?
A: Set the `enabled` attribute to `false` in the `exceptionless` config section.

## Q: Is there a minimum version of .NET you need to be targeting to use the Exceptionless client.
A: Yes, your application needs to be targeting .NET 3.5 or newer.

## Q: Can I use Exceptionless under medium trust?
A: Yes, you will need to set the `requirePermission` attribute to `false` in the `exceptionless` config section. This attribute allows the exceptionless client to read the exceptionless config settings. When you are running in medium trust, unhandled exceptions will not be caught. This means that you must [submit exceptions]({{ site.url }}/contents/sendingerrors) to Exceptionless manually.
