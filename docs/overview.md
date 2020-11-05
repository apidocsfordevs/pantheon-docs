---
title: Overview
---

With the Pantheon API, you can integrate with a variety of messaging platforms, allowing you to perform functions such as:
- caryying on a single conversation across multiple channels
- collecting payments via any of these channels
- authenticating users to your application from within their messaging app
- sending OTPs, and more.

The API uses RPC-style endpoints rather than REST-style resources. For instance, to start a conversation, the endpoint is POST http://pantheon.api/v1.0/conversations/startConversation. All endpoints accept a JSON body (or `multipart/form-data` where file uploads are allowed) and return a JSON response. The Pantheon API requires HTTPS (TLS 1.2 and above).

# Getting Started
To get started with the Pantheon API, you'll need a Pantheon app. Sign up to Pantheon, and create an app from your dashboard. You'll be provided credentials that identify your app (a client secret and client ID), and you can start to use these right away. For more on where to go next, see our [Getting Started guide](./guides/getting-started).

# Authentication
Pantheon uses OAuth2 for authentication. To authenticate your requests, pass in an `Authorization` header containing your access token prefixed by 'Bearer '. There's a detailed guide on authenticating, but here are the key facts:

To get a token, you'll need your app's client secret and ID from the dashboard.
1. Concatenate them in the format `your-client-id:your-client-secret`, and then encode with base64.
2. Make a POST request to http://pantheon.api/v1.0/auth/getAccessToken with the encoded value in an `Authorization` header (prefixed with `'Basic '`), and a body parameter `grant_type` set to "client_credentials". The response will contain an `access_token` valid for 4 hours (indicated in the `expires_in` parameter in the response) and a `refresh_token` that can be used to get a new token.

Here's an example of fetching an access token in Python:

```python
import requests
url = "http://pantheon.api/v1.0/auth/getAccessToken"
body = {"grant_type":"client_credentials"}
headers = {
    'authorization': "Basic SUtJQTFCNzU5M0M0NDAyQkM1RTAwQzQ2QUM4QjFDMUNDMEI4NUVFQkIwODg6c2VjcmV0",
    'content-type': "application/json"
}
response = requests.request("POST", url, data=body, headers=headers)
```

And an example response:

```json
{ 
  "access_token": "{Your access token}",
  "refresh_token": "{Your refresh token}",
  "token_type": "bearer",
  "expires_in": 86400
}
```

For a list of possible errors, see the section on [handling errors](#handling-errors). 

# Versioning
The Pantheon API requires a version number in URLs. The current version is 1.0. Breaking changes are only introduced in major versions (v1.0, v2.0, etc). Changes between versions, as well as migration guides, will be published on the [Changelog](./changelog) page.

# Rate Limiting
Most endpoints have an associated rate limit, described in the documentation for the endpoint. Rate limits are enforced on a per-account basis, and consist of an allotted number of API calls per minute. The limits will vary based on your Pantheon pricing plan.

Each API response will return the associated rate limits left for that endpoint and account. You can use this to check your rate limit status and adjust your requests accordingly.

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
X-RateLimit-Total: 700
X-RateLimit-Remaining: 426
```

- `X-RateLimit-Total` describes the total number of calls to this endpoint the account is allowed per minute
- `X-RateLimit-Remaining` describes the total number of calls to this endpoint the account has left in the current window

For more details, see the guide on [working around rate limits](./guides/working-with-rate-limits).

# Pagination
Pantheon uses cursor-based pagination. All endpoints that return a list of items will have their results wrapped in an `items` field. There will also be a `next_cursor` field that returns the full URL to the next set of results. If there are no more results, this field will be `null`. Check out our guide to [working with paginated results](./guides/pagination).

# Errors
Error responses returned by Pantheon will use standard HTTP codes. Here are the codes we currently use:
- `400`: Your request failed validation. You should check the `errors` field in the response, fix the errors and try again.
- `401`: The request was not authorized. You should double-check that you're using the proper credentials.
- `404`: The URL or resource was not found. You might have mistyped the URL or be requesting a deleted object.
- `500` - `504`: An error occurred on our end. Please report this using our [bug report tool](./pages/report-a-bug).

In addition to the status code, the response will also contain a `message` property and, for 400 errors, an `errors` key that lists out the specific items at fault.

Here's a sample error response:

```json
{
  "message": "Your request data was invalid.",
  "errors": [
    [
      "name": "The name field is required"
    ]
  ]
}
```

# Contact us
Got a question about the API or docs? Reach out to us on Twitter at @pantheonapi, or email us at api@pantheon.api.