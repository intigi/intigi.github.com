---
layout: default
---

## Welcome to the Intigi API documentation

Follow these steps to get started with the Intigi API:

1. [Sign up](https://intigi.com/start) for an Intigi account.
2. Set up your *Interests* and *Sources* in the Intigi web app.
3. Use the Intigi API to get a list of your [Interest Folders and Interests](/api-docs/v1/interest-folders-and-interests.html) in JSON format.
4. Use the Intigi API to get [Recommendations](/api-docs/v1/recommendations.html) in JSON format.

You can confirm that the API is operational by using the [Ping](/api-docs/v1/ping.html) endpoint.

### API Highlights

* API type: REST (JSON via HTTPS).
* Authentication: Via HTTP Basic Authentication.
* Rate limits: This is up to you since we charge for every request. Typical usage would be 1-50 requests per day and Interest.
* Security: All requests are performed via SSL. We properly encrypt all credentials on the wire and in the DB. We filter credentials so they never get stored in our server logs. Our firewalls are locked down tightly.

### API Concepts

* [Authentication](/api-docs/v1/authentication.html)
* [Interest Folders and Interests](/api-docs/v1/interest-folders-and-interests.html)
* [Ping](/api-docs/v1/ping.html)
* [Recommendations](/api-docs/v1/recommendations.html)
