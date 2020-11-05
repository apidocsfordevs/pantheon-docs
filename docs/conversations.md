---
title: Conversations v1.0
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - ruby: Ruby
  - python: Python
  - php: PHP
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="conversations">Conversations v1.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

The Conversations API provides a single entry point for users to carry out conversations across multiple supported messaging apps without losing any history.

Base URLs:

* <a href="http://pantheon.api/v1.0/conversations">http://pantheon.api/v1.0/conversations</a>

# Authentication

* API Key (Access Token)
    - Parameter Name: **Authorization**, in: header. 

<h1 id="conversations-engaging-in-conversations">Engaging in conversations</h1>

## Start a conversation

<a id="opIdStart a conversation"></a>

> Code samples

```shell
# You can also use wget
curl -X POST http://pantheon.api/v1.0/conversations/startConversation \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: API_KEY'

```

```http
POST http://pantheon.api/v1.0/conversations/startConversation HTTP/1.1
Host: pantheon.api
Content-Type: application/json
Accept: application/json

```

```javascript
const inputBody = '{
  "on": "SLACK",
  "with": "@shalvah"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'API_KEY'
};

fetch('http://pantheon.api/v1.0/conversations/startConversation',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'API_KEY'
}

result = RestClient.post 'http://pantheon.api/v1.0/conversations/startConversation',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'API_KEY'
}

r = requests.post('http://pantheon.api/v1.0/conversations/startConversation', headers = headers)

print(r.json())

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Content-Type' => 'application/json',
    'Accept' => 'application/json',
    'Authorization' => 'API_KEY',
);

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('POST','http://pantheon.api/v1.0/conversations/startConversation', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("http://pantheon.api/v1.0/conversations/startConversation");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"API_KEY"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "http://pantheon.api/v1.0/conversations/startConversation", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`POST /startConversation`

Begin a conversation via a supported messaging app.

Rate Limits:
- Test: 200 requests per minute
- Basic: 1000 requests per minute
- Premium: 10,000 requests per minute

Running a single conversation across multiple apps with Pantheon begins with a call to this endpoint. Check out our guide on [conversing with Pantheon](guides/conversing-with-pantheon).

> Body parameter

```json
{
  "on": "SLACK",
  "with": "@shalvah"
}
```

<h3 id="start-a-conversation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» on|body|string|true|ID of the application to begin the conversation on (eg Messenger, Twitter, SLack). Each app has a unique ID which can be retrieved from the [apps/getApps](./apps.md) endpoint.|
|» with|body|string|true|Identifier of the user on the provided messaging app.  This can be a username, phone number or ID.|

> Example responses

> OK

```json
{
  "conversationId": "jhyug498772hka"
}
```

<h3 id="start-a-conversation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|

<h3 id="start-a-conversation-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» conversationId|string|false|none|The ID of the started conversation. This ID can be used to track this conversation across all Pantheon endpoints.|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
Access Token
</aside>

## put__replyToConversation

> Code samples

```shell
# You can also use wget
curl -X PUT http://pantheon.api/v1.0/conversations/replyToConversation \
  -H 'Authorization: API_KEY'

```

```http
PUT http://pantheon.api/v1.0/conversations/replyToConversation HTTP/1.1
Host: pantheon.api

```

```javascript

const headers = {
  'Authorization':'API_KEY'
};

fetch('http://pantheon.api/v1.0/conversations/replyToConversation',
{
  method: 'PUT',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'API_KEY'
}

result = RestClient.put 'http://pantheon.api/v1.0/conversations/replyToConversation',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'API_KEY'
}

r = requests.put('http://pantheon.api/v1.0/conversations/replyToConversation', headers = headers)

print(r.json())

```

```php
<?php

require 'vendor/autoload.php';

$headers = array(
    'Authorization' => 'API_KEY',
);

$client = new \GuzzleHttp\Client();

// Define array of request body.
$request_body = array();

try {
    $response = $client->request('PUT','http://pantheon.api/v1.0/conversations/replyToConversation', array(
        'headers' => $headers,
        'json' => $request_body,
       )
    );
    print_r($response->getBody()->getContents());
 }
 catch (\GuzzleHttp\Exception\BadResponseException $e) {
    // handle exception or api errors.
    print_r($e->getMessage());
 }

 // ...

```

```java
URL obj = new URL("http://pantheon.api/v1.0/conversations/replyToConversation");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"API_KEY"},
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "http://pantheon.api/v1.0/conversations/replyToConversation", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`PUT /replyToConversation`

<h3 id="put__replytoconversation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
Access Token
</aside>

