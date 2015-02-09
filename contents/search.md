---
layout: docs
edit_path: search
title: Searching
prev_section: faq
permalink: /contents/search/
---

Here are some answers to frequently asked questions about Search.

## Q: Can I search by a wild card?
A: Yes, you need to prefix or suffix your query with a *

## Q: What fields can I search on?
A: 

###Stacks
<table class="table table-bordered">
  <thead>
    <tr>
      <th>Term</th>
      <th>Example</th>
      <th>Included In All</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">organization</th>
      <td>organization:54d8315ce6bb2d0500bcc7b4</td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">project</th>
      <td>project:54d8315ce6bb2d0500bcc7b4</td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">type</th>
      <td>type:error</td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">first</th>
      <td>first:date</td>
      <td>false</td>
      <td>first occurrence date</td>
    </tr>
    <tr>
      <th scope="row">last</th>
      <td>last:date</td>
      <td>false</td>
      <td>last occurrence date</td>
    </tr>
    <tr>
      <th scope="row">title</th>
      <td>title:"My Custom Log message" or "My Custom Log message"</td>
      <td>true</td>
      <td>The title of the stack</td>
    </tr>
    <tr>
      <th scope="row">description</th>
      <td>description:"My description" or "My Description"</td>
      <td>true</td>
      <td>The stack description</td>
    </tr>
    <tr>
      <th scope="row">tag</th>
      <td>tag:critical or critical</td>
      <td>true</td>
      <td>The stacks tags</td>
    </tr>
    <tr>
      <th scope="row">links</th>
      <td>links:"http://exceptionless.io" or "http://exceptionless.io"</td>
      <td>true</td>
      <td>The stacks reference links</td>
    </tr>
    <tr>
      <th scope="row">fixedon</th>
      <td>fixedon:date</td>
      <td>false</td>
      <td>The date the stack was marked as fixed</td>
    </tr>
    <tr>
      <th scope="row">fixed</th>
      <td>fixed:true</td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as fixed</td>
    </tr>
    <tr>
      <th scope="row">hidden</th>
      <td>hidden:true</td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as hidden</td>
    </tr>
    <tr>
      <th scope="row">regressed</th>
      <td>regressed:true</td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as regressed</td>
    </tr>
    <tr>
      <th scope="row">critical</th>
      <td>critical:true</td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as critical</td>
    </tr>
    <tr>
      <th scope="row">occurrences</th>
      <td>occurrences:50</td>
      <td>false</td>
      <td>The stacks total occurrences</td>
    </tr>
  </tbody>
</table>

###Events
<table class="table table-bordered">
  <thead>
    <tr>
      <th>Term</th>
      <th>Example</th>
      <th>Included In All</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">organization</th>
      <td>organization:54d8315ce6bb2d0500bcc7b4</td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">project</th>
      <td>project:54d8315ce6bb2d0500bcc7b4</td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">stack</th>
      <td>stack:54d8315ce6bb2d0500bcc7b4</td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">reference</th>
      <td>reference:12345678</td>
      <td>false</td>
      <td>The reference id</td>
    </tr>
    <tr>
      <th scope="row">session</th>
      <td>session:12345678</td>
      <td>false</td>
      <td>The session id</td>
    </tr>
    <tr>
      <th scope="row">type</th>
      <td>type:error</td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">source</th>
      <td>source:"my lof source" or "my log source"</td>
      <td>true</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">date</th>
      <td>date:date</td>
      <td>false</td>
      <td>The occurrence date</td>
    </tr>
    <tr>
      <th scope="row">message</th>
      <td>message:"My error message" or "My error message"</td>
      <td>true</td>
      <td>The message of the error</td>
    </tr>
    <tr>
      <th scope="row">tag</th>
      <td>tag:critical or critical</td>
      <td>true</td>
      <td>The stacks tags</td>
    </tr>
    <tr>
      <th scope="row">geo</th>
      <td>geo:coordinates</td>
      <td>false</td>
      <td>The geo location that the event occurrend in</td>
    </tr>
    <tr>
      <th scope="row">value</th>
      <td>value:1</td>
      <td>false</td>
      <td>The value associated to the event</td>
    </tr>
    <tr>
      <th scope="row">first</th>
      <td>first:true</td>
      <td>false</td>
      <td>returns all the first occurrences</td>
    </tr>
    <tr>
      <th scope="row">fixed</th>
      <td>fixed:true</td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as fixed</td>
    </tr>
    <tr>
      <th scope="row">hidden</th>
      <td>hidden:true</td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as hidden</td>
    </tr>
    <tr>
      <th scope="row">version</th>
      <td>version:1 or version:1.0 or version:1.0.0</td>
      <td>false</td>
      <td>The version of the app that created this event</td>
    </tr>
    <tr>
      <th scope="row">hidden</th>
      <td>hidden:true</td>
      <td>false</td>
      <td>The field will be set to true if the stack is marked as hidden</td>
    </tr>
    <tr>
      <th scope="row">machine</th>
      <td>machine:"Server" or "Server"</td>
      <td>true</td>
      <td>The machine name that created this event.</td>
    </tr>
    <tr>
      <th scope="row">ip</th>
      <td>ip:127.0.0.1 or 127.0.0.1</td>
      <td>true</td>
      <td>The IP address of the machine that created this event.</td>
    </tr>
    <tr>
      <th scope="row">architecture</th>
      <td>architecture:x64</td>
      <td>false</td>
      <td>The machine architecture that created this event.</td>
    </tr>
    <tr>
      <th scope="row">useragent</th>
      <td>useragent:IE</td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">path</th>
      <td>path:"/cart" or "/cart"</td>
      <td>true</td>
      <td>The url path that this event occurred on</td>
    </tr>
    <tr>
      <th scope="row">browser</th>
      <td>browser:"Chrome" or browser:"Chrome 50"</td>
      <td>false</td>
      <td>The browser</td>
    </tr>
    <tr>
      <th scope="row">browser.version</th>
      <td>browser.version:50.0</td>
      <td>false</td>
      <td>The browser version</td>
    </tr>
    <tr>
      <th scope="row">browser.major</th>
      <td>browser.major:50</td>
      <td>false</td>
      <td>The browser major version</td>
    </tr>
    <tr>
      <th scope="row">device</th>
      <td>device:iPhone</td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">os</th>
      <td>os:"iOS 8"</td>
      <td>false</td>
      <td>The operating system</td>
    </tr>
    <tr>
      <th scope="row">os.version</th>
      <td>os.version:8.0</td>
      <td>false</td>
      <td>The operating system version</td>
    </tr>
    <tr>
      <th scope="row">os.major</th>
      <td>os.major:8</td>
      <td>false</td>
      <td>The operating system major version</td>
    </tr>
    <tr>
      <th scope="row">bot</th>
      <td>bot:true</td>
      <td>false</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">error.code</th>
      <td>error.code:500 or 500</td>
      <td>true</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">error.message</th>
      <td>error.message:"A NullReferenceException occurred" or "A NullReferenceException occurred"</td>
      <td>true</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">error.type</th>
      <td>error.type:"System.NullReferenceException" or "System.NullReferenceException"</td>
      <td>true</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">user</th>
      <td>user:"random user identifier" or "random user identifier"</td>
      <td>true</td>
      <td>The identity assigned to the event.</td>
    </tr>
    <tr>
      <th scope="row">user.description</th>
      <td>user.description:"I clicked the button" or "I clicked the button"</td>
      <td>true</td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">user.email</th>
      <td>user.email:"support@exceptionless.io" or "support@exceptionless.io"</td>
      <td>true</td>
      <td></td>
    </tr>
  </tbody>
</table>
