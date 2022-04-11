---
title: Authentication
description: Discusses how user authentication is handled
date: 2022-04-10
tags:
  - Info
layout: layouts/post.njk
---

The user authentication service delivered by the `/auth` endpoint models an authentication service that would be available to connect the threaded-discussion application to other enterprise JWT based authentication platforms.

## Component

The `<jwt-auth>` web component allows users to log in to the authentication service. This authentication endpoint is defined by the `authendpoint` property of the tag. The state flow of the tag is as follows:

1. The tag checks LocalStorage for a JWT in the `comment-jwt` tag. If the value is present, the tag enters the "authenticated" state and emits an `auth-success` event.
2. The tag is rendered on the page. If the tag is in the authenticated state, the tag does not appear. If the tag is not in the authenticated state, it displays a login prompt on the screen
3. The user authenticates with the authentication service.
4. The tag receives the JWT returned by the service and creates a new localStorage entry under `comment-jwt`. At this point the tag enters the authenticated state and emits an `auth-success` event.

The component is integrated into the `threaded-discussion` component by adding placing the `jwt-auth` component inside it and adding an event listener to the parent for `auth-success` events. Listening to these events allows the comment engine to enable/disable itself.

[View the component source code here](https://github.com/mayormaier/jwt-auth-component)
[View the npm package here](https://www.npmjs.com/package/jwt-auth-component)

## Security Considerations

At the current moment, there are some serious security considerations with this component. Firstly, there is no password field on the login page. This is problematic for obvious reasons.

In reading, I found multiple sources reporting that it is insecure to store JWTs directly in LocalStorage. There are alternative methods to prevent against XSS and CSRF attacks. These should be investigated in the future

There is no support currently for MFA, although this would most likely be implemented by the authentication provider.
