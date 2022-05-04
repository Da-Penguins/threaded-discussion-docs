---
title: Multithreading
description: How does <threaded-discussion> enable the user to use multiple comment blocks on a single page?
date: 2022-05-03
tags:
  - Info
layout: layouts/post.njk
---
The `threaded-discussion` web component enables users to place multiple comment blocks on a single page- each with their own set of comments that are completely isolated from each other.

## What makes discussions unique?

Each thread has a unique id which is referenced by the `uid` attribute (ThreadID property) of the component. Threads must be created outside of the page that they were placed on, so that the component can be inserted onto the destination HTML page on the server-side.

Note that in the demo, the `<thread-creator>` component accomplishes this task of creating threads- although the threads that it creates are short lived, and will be removed from the DOM when the page reloads. This `<thread-creator>` component interacts with the `create-thread` API to create the thread record in the database.

After the API creates the database record for the new comment thread, it returns the ID of the thread as well as the valid domain and permissions for validation by the front end.

> NOTE: New threads may only be created by admin users. Use the following JWT in the `comment-jwt` value in LocalStorage to test this feature.
> eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImRlbW8tYWRtaW4iLCJ1aWQiOiIxMjU4ZDIwYy00NGQ3LTRlNGMtODlhYy0zMTE1YmM4YmUwNjYiLCJpc0FkbWluIjp0cnVlLCJpYXQiOjE2NTE2MjUyNDZ9.XyoPq4xliV7s-467G-U4dHv7_yiFxJAqIewLFJR60yM

Additionally, note that the creation of new threads does not occur automatically when the component is placed on a page/rendered. In a production scenario, a separate system (i.e., WYSISYG editor) would work to generate these new threads and insert their respective UUIDs into the `<threaded-discussion>` `uid` attribute.

## How are discussions tied to a particular page?

When the thread is created, the client must provide the `href` of the page where the discussion will be placed. This value is checked against the `referrer` header of an incoming web request- so that the tag can only be placed on authorized pages.

In the demo, discussion block 3 is not visible to users as it is tied to the `localhost:3000/` page. Thus, the element is unable to load the comments from this discussion with the `get-comment` API unless the `referrer` header of the request is `localhost:3000/`. On the other hand, discussions one and two in the demo are visible, as they are not tied to any page. So, when the comments for these discussions are requested, they are able to load.
