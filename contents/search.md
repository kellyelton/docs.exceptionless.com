---
layout: docs
edit_path: search
title: Searching
prev_section: faq
permalink: /contents/search/
---

Here are some answers to frequently asked questions about Search.

## Q: Can I search by multiple queries?
**A:** Yes, all queries separated by a space will be an `AND` operation. If you wish to `OR` queries you'll need to use an `OR` statement (Ex. `tag:blue OR tag:red`).

## Q: Can I search by a wild card?
**A:** Yes, you need to suffix your query with a `*`

## Q: Can I search with an exclusion?
**A:** Yes, you need to prefix the field name with `-`.

**Example:** Lets assume that we want to return all events that are not marked as a bot. To search for these events our query would be `-bot:true`. *NOTE: In some cases searching with `-bot:true` is more accurate than searching with `bot:false`. This happens because the first query returns all records where `bot` field is `not set` or `not equal to true`. The second query returns results only where the `bot` field is set to `false`.

## Q: Can I search for set and unset fields?
**A:** Yes, you need to prefix the field name with `_missing_` or `_exists_`.

**Example:** Lets assume that we want to return all events that do not contain any tags. To search for these events our query would be `_missing_:tag`

## Q: Can I search by using ranges?
**A:** Yes, you need to specify a `date` or `numeric` range as part of the term. Please see [this](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html#_ranges_2) for more information.

**Date Range Example:** Lets assume that we want to return all events that occurred in 2020. To search for these events our query would be `date:[2020-01-01 TO 2020-12-31]`.

**Numeric Range Example:** Lets assume that we want to return all events that contain contain a `value` between 1 and 10. To search for these events our query would be `value:(>0 AND <=10)`.

## Q: Can I search by my custom extended data?
**A:** Yes, all simple data types (`string`, `boolean`, `date`, `number`) that are stored in extended data will be indexed. *NOTE: Field names will be lowercased and escaped. If your field contains a `space` it will be escaped with a `-`.* 

**Example:** Lets assume that our events extended data contains a property called `Age` with a value of `18`. To search for this value our query would be `data.age:18`.

## Q: What fields can I search on?
**A:** 

<table class="table table-bordered">
  <thead>
    <tr>
      <th>Term</th>
      <th>Example</th>
      <th>field required (field:term)</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">id</th>
      <td><code>id:54d8315ce6bb2d0500bcc7b4</code></td>
      <td>true</td>
      <td>The documents id</td>
    </tr>
    <tr>
      <th scope="row">organization</th>
      <td><code>organization:54d8315ce6bb2d0500bcc7b4</code></td>
      <td>true</td>
      <td>Organization id</td>
    </tr>
    <tr>
      <th scope="row">project</th>
      <td><code>project:54d8315ce6bb2d0500bcc7b4</code></td>
      <td>true</td>
      <td>Project id</td>
    </tr>
    <tr>
      <th scope="row">stack</th>
      <td><code>stack:54d8315ce6bb2d0500bcc7b4</code></td>
      <td>true</td>
      <td>Stack id</td>
    </tr>
    <tr>
      <th scope="row">reference</th>
      <td><code>reference:12345678</code></td>
      <td>true</td>
      <td>Reference id</td>
    </tr>
    <tr>
      <th scope="row">session</th>
      <td><code>session:12345678</code></td>
      <td>true</td>
      <td>Session id</td>
    </tr>
    <tr>
      <th scope="row">type</th>
      <td><code>type:error</code></td>
      <td>true</td>
      <td>Event type</td>
    </tr>
    <tr>
      <th scope="row">source</th>
      <td><code>source:"my log source"</code> or <code>"my log source"</code></td>
      <td>false</td>
      <td>Event source</td>
    </tr>
    <tr>
      <th scope="row">level</th>
      <td><code>level:Error</code></td>
      <td>true</td>
      <td>Log level</td>
    </tr>
    <tr>
      <th scope="row">date</th>
      <td><code>date:"2020-10-16T12:00:00.000"</code></td>
      <td>true</td>
      <td>Occurrence date</td>
    </tr>
    <tr>
      <th scope="row">first</th>
      <td><code>first:true</code></td>
      <td>true</td>
      <td>True if it's the first occurrence of an event</td>
    </tr>
    <tr>
      <th scope="row">message</th>
      <td><code>message:"My error message"</code> or <code>"My error message"</code></td>
      <td>false</td>
      <td>Event message</td>
    </tr>
    <tr>
      <th scope="row">tag</th>
      <td><code>tag:"Blake Niemyjski"</code> or<code>tag:Blake</code> or <code>blake</code></td>
      <td>false</td>
      <td>Tags</td>
    </tr>
    <tr>
      <th scope="row">value</th>
      <td><code>value:1</code></td>
      <td>true</td>
      <td>Value of the event (used in charts)</td>
    </tr>
    <tr>
      <th scope="row">fixed</th>
      <td><code>fixed:true</code></td>
      <td>true</td>
      <td>True if marked as fixed</td>
    </tr>
    <tr>
      <th scope="row">hidden</th>
      <td><code>hidden:true</code></td>
      <td>true</td>
      <td>True if marked as hidden</td>
    </tr>
    <tr>
      <th scope="row">version</th>
      <td><code>version:1</code> or <code>version:1.0</code> or <code>version:1.0.0</code></td>
      <td>true</td>
      <td>Application version</td>
    </tr>
    <tr>
      <th scope="row">machine</th>
      <td><code>machine:Server</code> or <code>Server</code></td>
      <td>false</td>
      <td>Machine name</td>
    </tr>
    <tr>
      <th scope="row">ip</th>
      <td><code>ip:127.0.0.1</code> or <code>127.0.0.1</code></td>
      <td>false</td>
      <td>IP address</td>
    </tr>
    <tr>
      <th scope="row">architecture</th>
      <td><code>architecture:x64</code></td>
      <td>true</td>
      <td>Machine architecture</td>
    </tr>
    <tr>
      <th scope="row">useragent</th>
      <td><code>useragent:IE</code> or <code>useragent:"Mozilla/5.0"</code></td>
      <td>true</td>
      <td>User Agent</td>
    </tr>
    <tr>
      <th scope="row">path</th>
      <td><code>path:"/cart"</code> or <code>"/cart"</code></td>
      <td>false</td>
      <td>Url path</td>
    </tr>
    <tr>
      <th scope="row">browser</th>
      <td><code>browser:Chrome</code></td>
      <td>true</td>
      <td>Browser</td>
    </tr>
    <tr>
      <th scope="row">browser.version</th>
      <td><code>browser.version:50.0</code></td>
      <td>true</td>
      <td>Browser version</td>
    </tr>
    <tr>
      <th scope="row">browser.major</th>
      <td><code>browser.major:50</code></td>
      <td>true</td>
      <td>Browser major version</td>
    </tr>
    <tr>
      <th scope="row">device</th>
      <td><code>device:iPhone</code></td>
      <td>true</td>
      <td>Device</td>
    </tr>
    <tr>
      <th scope="row">os</th>
      <td><code>os:iOS</code></td>
      <td>true</td>
      <td>Operating System</td>
    </tr>
    <tr>
      <th scope="row">os.version</th>
      <td><code>os.version:8.0</code></td>
      <td>true</td>
      <td>Operating System version</td>
    </tr>
    <tr>
      <th scope="row">os.major</th>
      <td><code>os.major:8</code></td>
      <td>true</td>
      <td>Operating System major version</td>
    </tr>
    <tr>
      <th scope="row">bot</th>
      <td><code>bot:true</code></td>
      <td>true</td>
      <td>Bot</td>
    </tr>
    <tr>
      <th scope="row">error.code</th>
      <td><code>error.code:500</code> or <code>500</code></td>
      <td>false</td>
      <td>Error code</td>
    </tr>
    <tr>
      <th scope="row">error.message</th>
      <td><code>error.message:"A NullReferenceException occurred"</code> or <code>"A NullReferenceException occurred"</code></td>
      <td>false</td>
      <td>Error message</td>
    </tr>
    <tr>
      <th scope="row">error.type</th>
      <td><code>error.type:"System.NullReferenceException"</code> or <code>"System.NullReferenceException"</code></td>
      <td>false</td>
      <td>Error type</td>
    </tr>
    <tr>
      <th scope="row">error.targettype</th>
      <td><code>error.targettype:"System.NullReferenceException"</code> or <code>"System.NullReferenceException"</code></td>
      <td>false</td>
      <td>Error target type</td>
    </tr>
    <tr>
      <th scope="row">error.targetmethod</th>
      <td><code>error.targetmethod:AssociateWithCurrentThread</code> or <code>AssociateWithCurrentThread</code></td>
      <td>false</td>
      <td>Error target method</td>
    </tr>
    <tr>
      <th scope="row">user</th>
      <td><code>user:"random user identifier"</code> or <code>"random user identifier"</code></td>
      <td>false</td>
      <td>Uniquely identifies the user.</td>
    </tr>
   <tr>
    <tr>
      <th scope="row">user.name</th>
      <td><code>user:"Exceptionless User"</code> or <code>"Exceptionless User"</code></td>
      <td>false</td>
      <td>Friendly name of the user.</td>
    </tr>
    <tr>
      <th scope="row">user.description</th>
      <td><code>user.description:"I clicked the button"</code> or <code>"I clicked the button"</code></td>
      <td>false</td>
      <td>User Description</td>
    </tr>
    <tr>
      <th scope="row">user.email</th>
      <td><code>user.email:"support@exceptionless.io"</code> or <code>"support@exceptionless.io"</code></td>
      <td>false</td>
      <td>User Email Address</td>
    </tr>
  </tbody>
</table>
