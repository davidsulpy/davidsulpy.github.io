---
layout: post
title: "Authentication with RESTful APIs Done Right"
date: 2013-12-05 10:15
comments: true
published: false
categories: ["REST", "API", "Security"]
---

Authenitcation is an important part of having valuable accessible resources. If something is not available for use, it's arguable hack proof, but not necessisarily secure. So to maintain integrity, confidentiality and value of resources exposed through an API for instance, it's important to implement the right authentication approach for the right risk acceptance level. Here I'll show two methods to do API Authentication for RESTful/stateless APIs without giving away the goods.

##Method 1 (API Key + Auth Token)
This is the least secure of the two, but it's also the simplest and therefore, if you have a low risk API or a high risk acceptance, this might be the right business decision for securing your API. Only you can make that decision.

The general idea is as follows:
>Issue a semi-private API Key specific to the client or group accessing the API, then you issue an expiring authentication token per username/password authenitcation call. This authenitcation token is then used for every subsequent call after the authentication call to provide better assurance that the user is who they say they are.

Here is a more detailed workflow with some explination along the way:
####1. Issue API Key
This can be a guid or a cryptographically secure key that you issue to clients. It's semi-secure because it's possibly shared amongst applications accessing the API and therefore shared amongst an organization or group outside the control of the issuing party. It is, however, usable for revoking access to an entire group or application or throttling use/tracking usability. Once an API Key has been delivered to a consuming application