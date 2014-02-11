---
layout: docs
edit_path: security
title: Security
prev_section: sendingerrors
next_section: troubleshooting
permalink: /contents/configuration/
---

Exceptionless follows industry best practices and uses SSL out of the box to be as secure as possible. We provide you with the tools to take your information secruity to the next level.

## Data Exclusions

A comma delimited list of field names that should be removed from any error report data (e.g., extended data properties, form fields, cookies and query parameters). Data Exclusions can be configured on the project settings page. You can also specify a field name with a wildcard (*) to specify starts with, ends with, or contains just to be extra safe.

###Example usage:
1. Entering `Password` will remove any field **named** `Password` from the report.
2. Entering `Password*` will remove any field that **starts with** `Password` from the report.
3. Entering `*Password` will remove any field that **ends with** `Password` from the report.
4. Entering `*Password*` will remove any field that **contains** `Password` from the report.
