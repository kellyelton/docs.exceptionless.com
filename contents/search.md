---
layout: docs
edit_path: search
title: Searching
prev_section: faq
permalink: /contents/search/
---

Here are some answers to frequently asked questions about Search.

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
  </tbody>
</table>
