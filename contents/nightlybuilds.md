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

NuGet can display packages from multiple package sources. To add a package source, you must first open the **Manage NuGet Packages** dialog. 

![Manage NuGet Packages"](../../images/nightlybuilds/manage.nuget.packages.png "Manage NuGet Packages")

Next, click on the settings button to launch the options dialog. Make sure the **Package Sources** node is selected in the dialog.

![Package Sources](../../images/nightlybuilds/package.sources.png "Package Sources")

Click the add button, located in the upper righthand side of the dialog to add a new package source. Create the package source with the name: **Exceptionless Nightly Builds** and source: **https://www.myget.org/F/exceptionless/**

![Manage NuGet Packages Nightly Builds](../../images/nightlybuilds/manage.nuget.packages.nightly.png "Manage NuGet Packages Nightly Builds")

Next, click the Update button to apply the changes and click the OK button to go back to the **Manage NuGet Packages** dialog. 

Finally, select the **Exceptionless Nightly Builds** node. Your now all set to install or update to the latest nightly build of exceptionless.

**If you use a build server, you may also have to add https://www.myget.org/F/exceptionless/ as a package source in your  [NuGet config settings](http://docs.nuget.org/docs/reference/nuget-config-settings).**

## Using stable builds

In the event that you want to go to stable builds, you just need to ensure that you are grabbing the latest build from the .nuget node in the **Manage NuGet Packages** dialog. It is also safe to delete the **Exceptionless Nightly Builds** package source.
