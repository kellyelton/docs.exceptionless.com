---
layout: docs
edit_path: nightlybuilds
title: Nightly Builds
prev_section: home
next_section: home
permalink: /contents/nightlybuilds/
---

The following section will guide you through getting nightly builds by using our external NuGet feed.

Please see the official [NuGet documentation](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog "NuGet documentation") for more information.

## Consuming nightly builds

NuGet can display packages from multiple package sources. To add a package source, you must first open the "Manage NuGet Packages" dialog. 

![Manage NuGet Packages"](/images/nightlybuilds/manage.nuget.packages.png "Manage NuGet Packages")

Next, click on the Settings button in the dialog to launch the Options dialog. Make sure the Package Sources node is selected in the dialog.

![Package Sources](/images/nightlybuilds/package.sources.png "Package Sources")

Click the add button and add a new package source with the name "Exceptionless Nightly Builds" and a Source (https://www.myget.org/F/exceptionless/)

![Manage NuGet Packages Nightly Builds](/images/nightlybuilds/manage.nuget.packages.nightly.png "Manage NuGet Packages Nightly Builds")

Next click OK and go back to the "Manage NuGet Packages" dialog and select the "Exceptionless Nightly Builds" node.

Your now all set to install the latest nightly build of exceptionless or update from a stable build to a nightly build.

**If you use a build server, you may also have to add (https://www.myget.org/F/exceptionless/) as a package source in your ![NuGet config settings](http://docs.nuget.org/docs/reference/nuget-config-settings "NuGet config settings").**

## Using stable builds

In the event that you want to go to stable builds, you just need to ensure that you are grabbing the latest build from the .nuget node in the "Manage NuGet Packages" dialog. It is also safe to delete the "Exceptionless Nightly Builds" package source.
