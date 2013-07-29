---
layout: docs
title: Configuration
prev_section: gettingstarted
next_section: sendingerrors
permalink: /contents/configuration/
---

Exceptionless is configured using a config section in your web.config or app.config depending on what kind of
project you have. Installing the correct NuGet package should automatically add the necessary configuration
elements.  It should look like this:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <configSections>
    <section name="exceptionless" type="Exceptionless.Configuration.ExceptionlessSection, Exceptionless" />
  </configSections>
  <!-- attribute names are cases sensitive, must specify a path that you have write access to -->
  <exceptionless apiKey="API_KEY_HERE" enableLogging="true" logPath="C:\log.txt" />
  ...
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false" />
    <modules>
      <remove name="ExceptionlessModule" />
      <add name="ExceptionlessModule" type="Exceptionless.Mvc.ExceptionlessModule, Exceptionless.Mvc" />
    </modules>
    ...
  </system.webServer>
</configuration>
```
