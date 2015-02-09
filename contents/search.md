---
layout: docs
edit_path: search
title: Searching
prev_section: faq
permalink: /contents/search/
---

Here are some answers to frequently asked questions about Search.

## Q: Can I search by a wild card?
A: Yes, you need to suffix your query with a *

## Q: What fields can I search on?
A: 

####Stacks
<table class="table table-bordered">
  <thead>
    <tr>
      <th>Term</th>
      <th>Example</th>
      <th>field is optional (field:term)</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">organization</th>
      <td><code>organization:54d8315ce6bb2d0500bcc7b4</code></td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">project</th>
      <td><code>project:54d8315ce6bb2d0500bcc7b4</code></td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">type</th>
      <td><code>type:error</code></td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">first</th>
      <td><code>first:date</code></td>
      <td>false</td>
      <td>first occurrence date</td>
    </tr>
    <tr>
      <th scope="row">last</th>
      <td><code>last:date</code></td>
      <td>false</td>
      <td>last occurrence date</td>
    </tr>
    <tr>
      <th scope="row">title</th>
      <td><code>title:"My Custom Log message"</code> or <code>"My Custom Log message"</code></td>
      <td>true</td>
      <td>The title of the stack</td>
    </tr>
    <tr>
      <th scope="row">description</th>
      <td><code>description:"My description"</code> or <code>"My Description"</code></td>
      <td>true</td>
      <td>The stack description</td>
    </tr>
    <tr>
      <th scope="row">tag</th>
      <td><code>tag:critical</code> or <code>critical</code></td>
      <td>true</td>
      <td>The stacks tags</td>
    </tr>
    <tr>
      <th scope="row">links</th>
      <td><code>links:"http://exceptionless.io"</code> or <code>"http://exceptionless.io"</code></td>
      <td>true</td>
      <td>The stacks reference links</td>
    </tr>
    <tr>
      <th scope="row">fixedon</th>
      <td><code>fixedon:date</code></td>
      <td>false</td>
      <td>The date the stack was marked as fixed</td>
    </tr>
    <tr>
      <th scope="row">fixed</th>
      <td><code>fixed:true</code></td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as fixed</td>
    </tr>
    <tr>
      <th scope="row">hidden</th>
      <td><code>hidden:true</code></td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as hidden</td>
    </tr>
    <tr>
      <th scope="row">regressed</th>
      <td><code>regressed:true</code></td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as regressed</td>
    </tr>
    <tr>
      <th scope="row">critical</th>
      <td><code>critical:true</code></td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as critical</td>
    </tr>
    <tr>
      <th scope="row">occurrences</th>
      <td><code>occurrences:50</code></td>
      <td>false</td>
      <td>The stacks total occurrences</td>
    </tr>
  </tbody>
</table>

####Events
<table class="table table-bordered">
  <thead>
    <tr>
      <th>Term</th>
      <th>Example</th>
      <th>field is optional (field:term)</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">organization</th>
      <td><code>organization:54d8315ce6bb2d0500bcc7b4</code></td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">project</th>
      <td><code>project:54d8315ce6bb2d0500bcc7b4</code></td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">stack</th>
      <td><code>stack:54d8315ce6bb2d0500bcc7b4</code></td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">reference</th>
      <td><code>reference:12345678</code></td>
      <td>false</td>
      <td>The reference id</td>
    </tr>
    <tr>
      <th scope="row">session</th>
      <td><code>session:12345678</code></td>
      <td>false</td>
      <td>The session id</td>
    </tr>
    <tr>
      <th scope="row">type</th>
      <td><code>type:error</code></td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">source</th>
      <td><code>source:"my lof source"</code> or <code>"my log source"</code></td>
      <td>true</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">date</th>
      <td><code>date:date</code></td>
      <td>false</td>
      <td>The occurrence date</td>
    </tr>
    <tr>
      <th scope="row">message</th>
      <td><code>message:"My error message"</code> or <code>"My error message"</code></td>
      <td>true</td>
      <td>The message of the error</td>
    </tr>
    <tr>
      <th scope="row">tag</th>
      <td><code>tag:critical</code> or <code>critical</code></td>
      <td>true</td>
      <td>The stacks tags</td>
    </tr>
    <tr>
      <th scope="row">geo</th>
      <td><code>geo:coordinates</code></td>
      <td>false</td>
      <td>The geo location that the event occurrend in</td>
    </tr>
    <tr>
      <th scope="row">value</th>
      <td><code>value:1</code></td>
      <td>false</td>
      <td>The value associated to the event</td>
    </tr>
    <tr>
      <th scope="row">first</th>
      <td><code>first:true</code></td>
      <td>false</td>
      <td>returns all the first occurrences</td>
    </tr>
    <tr>
      <th scope="row">fixed</th>
      <td><code>fixed:true</code></td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as fixed</td>
    </tr>
    <tr>
      <th scope="row">hidden</th>
      <td><code>hidden:true</code></td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as hidden</td>
    </tr>
    <tr>
      <th scope="row">version</th>
      <td><code>version:1</code> or <code>version:1.0</code> or <code>version:1.0.0</code></td>
      <td>false</td>
      <td>The version of the app that created this event</td>
    </tr>
    <tr>
      <th scope="row">hidden</th>
      <td><code>hidden:true</code></td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as hidden</td>
    </tr>
    <tr>
      <th scope="row">machine</th>
      <td><code>machine:Server</code> or <code>Server</code></td>
      <td>true</td>
      <td>The machine name that created this event.</td>
    </tr>
    <tr>
      <th scope="row">ip</th>
      <td><code>ip:127.0.0.1</code> or <code>127.0.0.1</code></td>
      <td>true</td>
      <td>The IP address of the machine that created this event.</td>
    </tr>
    <tr>
      <th scope="row">architecture</th>
      <td><code>architecture:x64</code></td>
      <td>false</td>
      <td>The machine architecture that created this event.</td>
    </tr>
    <tr>
      <th scope="row">useragent</th>
      <td><code>useragent:IE</code></td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">path</th>
      <td><code>path:"/cart"</code> or <code>"/cart"</code></td>
      <td>true</td>
      <td>The url path that this event occurred on</td>
    </tr>
    <tr>
      <th scope="row">browser</th>
      <td><code>browser:Chrome</code></td>
      <td>false</td>
      <td>The browser</td>
    </tr>
    <tr>
      <th scope="row">browser.version</th>
      <td><code>browser.version:50.0</code></td>
      <td>false</td>
      <td>The browser version</td>
    </tr>
    <tr>
      <th scope="row">browser.major</th>
      <td><code>browser.major:50</code></td>
      <td>false</td>
      <td>The browser major version</td>
    </tr>
    <tr>
      <th scope="row">device</th>
      <td><code>device:iPhone</code></td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">os</th>
      <td><code>os:"iOS 8"</code></td>
      <td>false</td>
      <td>The operating system</td>
    </tr>
    <tr>
      <th scope="row">os.version</th>
      <td><code>os.version:8.0</code></td>
      <td>false</td>
      <td>The operating system version</td>
    </tr>
    <tr>
      <th scope="row">os.major</th>
      <td><code>os.major:8</code></td>
      <td>false</td>
      <td>The operating system major version</td>
    </tr>
    <tr>
      <th scope="row">bot</th>
      <td><code>bot:true</code></td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">error.code</th>
      <td><code>error.code:500</code> or <code>500</code></td>
      <td>true</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">error.message</th>
      <td><code>error.message:"A NullReferenceException occurred"</code> or <code>"A NullReferenceException occurred"</code></td>
      <td>true</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">error.type</th>
      <td><code>error.type:"System.NullReferenceException"</code> or <code>"System.NullReferenceException"</code></td>
      <td>true</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">user</th>
      <td><code>user:"random user identifier"</code> or <code>"random user identifier"</code></td>
      <td>true</td>
      <td>The identity assigned to the event.</td>
    </tr>
    <tr>
      <th scope="row">user.description</th>
      <td><code>user.description:"I clicked the button"</code> or <code>"I clicked the button"</code></td>
      <td>true</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">user.email</th>
      <td><code>user.email:"support@exceptionless.io"</code> or <code>"support@exceptionless.io"</code></td>
      <td>true</td>
      <td></td>
    </tr>
  </tbody>
</table>
