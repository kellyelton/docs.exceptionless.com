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


