---
layout: docs
edit_path: faq
title: Frequently Asked Questions
prev_section: troubleshooting
next_section: upgrading
permalink: /contents/faq/
---

Here are some answers to frequently asked questions about the Exceptionless service.

## Q: Will Exceptionless slow my application down?
A: Exceptionless queues all events submissions to disk and then processes them in a background thread. We do
everything we can to make sure that we do not slow your app down or crash your app. *NOTE: If you are sending a very large amount of events, we recommend using [in memory storage]({{ site.url }}/contents/configuration) as this will prevent events from being stored on disk.*

## Q: What will happen if my application throws a bunch of exceptions in a very short amount of time?
A: Exceptionless will intelligently try to ensure that the right amount of data is sent in. First, the client will ensure that the same error occurrence isn't submitted repeatedly by multiple error handlers within a very small window of time (E.G., Two seconds). Finally, in some cases the server logic will step in to remove error occurrences that it feels are spam. For example: Your site might be scanned by a bot and throw a bunch of unique 404 errors. Our system will see all of these within a small window of time submitted by a specific IP address. Once it hits a configurable threshold of error occurrences within a specific amount of time, these error occurrences will be removed from the system.

## Q: Can I reset my event data?
A: You can reset your event data at the project level by going into the manage project page and clicking the `Reset Project Data` button. You can also delete all event data for a specific stack by going to the stack page, clicking the `Options` button and clicking `Delete`.

## Q: What happens if my internet connection goes down?
A: Exceptionless queues all events submissions to disk and will retry them later.

## Q: How can I disable event reporting during testing?
A: Set the `enabled` attribute to `false` in the `exceptionless` config section.

## Q: Is there a minimum version of .NET you need to be targeting to use the Exceptionless client.
A: Yes, your application needs to be targeting .NET 4.0 or newer.

## Q: Can I use Exceptionless under medium trust?
A: Yes, you will need to set the `requirePermission` attribute to `false` in the `exceptionless` config section. This attribute allows the exceptionless client to read the exceptionless config settings. When you are running in medium trust, unhandled exceptions will not be caught. This means that you must [submit exceptions]({{ site.url }}/contents/sendingevents) to Exceptionless manually.
