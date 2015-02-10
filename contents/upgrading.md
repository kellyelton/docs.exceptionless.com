---
layout: docs
edit_path: upgrading
title: Upgrading the Exceptionless client
prev_section: faq
permalink: /contents/upgrading/
---

##Upgrading from all previous versions of Exceptionless
Please read this guide when upgrading from any version of Exceptionless.

1. Open the NuGet Package Manager dialog.
2. Click on the Updates tab.
3. *NOTE: To upgrade to 2.x preview you will have to select "Include Prerelease" from the dropdown.*
4. Select the exceptionless nuget packages and click the Update button.

For more information please see the official [NuGet documentation](https://docs.nuget.org/consume/Package-Manager-Dialog).

##Upgrading from Exceptionless 1.x

Please read this guide when upgrading from Exceptionless 1.x. The Exceptionless latest client has a few breaking changes from 1.x client that users users should be aware of when upgrading. Please follow the guide below after upgrading your NuGet packages from version 1.x to the latest version.

### Exceptionless client changes
<table class="table table-bordered">
  <thead>
    <tr>
      <th>Old Name</th>
      <th>New Name</th>
      <th>Action</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row"><code>ExceptionlessClient.Current</code></th>
      <td><code>ExceptionlessClient.Default</code></td>
      <td>Rename</td>
      <td><code>Exceptionless.Current</code> has been deprecated.</td>
    </tr>
    <tr>
      <th scope="row"><code>ErrorBuilder</code></th>
      <td><code>EventBuilder</code></td>
      <td>Rename</td>
      <td>Error methods has been renamed.</td>
    </tr>
    <tr>
      <th scope="row"><code>queuePath</code></th>
      <td><code>storagePath</code></td>
      <td>Rename</td>
      <td>Attribute and xml configuration attributes have been renamed.</td>
    </tr>
    <tr>
      <th scope="row"><code>extendedData</code></th>
      <td><code>data</code></td>
      <td>Rename</td>
      <td>Attribute and xml configuration attributes have been renamed.</td>
    </tr>
    <tr>
      <th scope="row"><code>ExceptionlessAttribute(params)</code></th>
      <td><code>ExceptionlessAttribute(string apiKey, EnableSSL = true)</code></td>
      <td>Update</td>
      <td>Attribute configuration overloads has been removed in favor of object initializers.</td>
    </tr>
    <tr>
      <th scope="row"><code>event UnhandledExceptionReporting</code></th>
      <td><code>event SubmittingEvent</code></td>
      <td>Update</td>
      <td>Wire up to <code>SubmittingEvent</code> and check the <code>IsUnhandledError</code> property. <i>NOTE: Error has been renamed to Event on the Event Args class.</i></td>
    </tr>
    <tr>
      <th scope="row"><code>ExceptionlessClient.Current.GetLastErrorId()</code></th>
      <td><code>ExceptionlessClient.Default.GetLastReferenceId()</code></td>
      <td>Rename</td>
      <td>This method has been renamed. NOTE: to have a reference id automatically generated you must call <code>ExceptionlessClient.Default.Configuration.UseReferenceIds()</code></td>
    </tr>
    <tr>
      <th scope="row"><code>event RequestSending</code></th>
      <td></td>
      <td>Remove</td>
      <td>Implement custom <code>ISubmissionClient</code> and register it with the dependency resolver.</td>
    </tr>
    <tr>
      <th scope="row"><code>event SendErrorCompleted</code></th>
      <td></td>
      <td>Remove</td>
      <td>Implement custom <code>ISubmissionClient</code> and register it with the dependency resolver.</td>
    </tr>
  </tbody>
</table>

*Please contact support for assistance on updating any undocumented upgrade changes.*
