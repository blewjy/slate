
## Camera Providers

Camera providers are companies/brands that supply cameras to consumers. The Fleet APIs allow you to manage your company's camera providers, with each `camera_provider` object having the following properties:

| Property             | Type   | Description                          |
| -------------------- | ------ | ------------------------------------ |
| `name`               | String | Name of the camera provider          |
| `camera_provider_id` | String | A unique camera provider ID          |
| `brand`              | String | Brand name of the camera provider    |
| `country`            | String | Country of origin of camera provider |

### Get all camera providers

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/fleet/camera-providers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/camera-providers', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/camera-providers' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/camera-providers',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

> 200 Response

```json
{
  "success": true,
  "data": [
    {
      "name": "GoPro, Inc.",
      "camera_provider_id": "6811b8e899b9e7207775390d9664181b",
      "brand": "GoPro",
      "country": "USA"
    }
  ]
}
```

`GET /fleet/camera-providers`

Get all cameras providers belonging to the company of the user. The response returns an array of all the `camera_provider` objects that belong to your company.

<div></div>

### Create new camera provider

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.garuda.io/v2/fleet/camera-providers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json'
}

r = requests.post('https://api.garuda.io/v2/fleet/camera-providers', params={

}, headers = headers)

print r.json()

```

```shell
curl -X POST 'https://api.garuda.io/v2/fleet/cameras-providers' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "name": "GoPro, Inc.",
      "brand": "GoPro",
      "country": "USA"
     }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "name": "GoPro, Inc.",
  "brand": "GoPro",
  "country": "USA"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/camera-providers',
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

> 200 Response

```json
{
  "success": true,
  "data": {
    "name": "GoPro, Inc.",
    "camera_provider_id": "6811b8e899b9e7207775390d9664181b",
    "brand": "GoPro",
    "country": "USA"
  }
}
```

`POST /fleet/camera-providers`

Create a new camera provider belonging to the company of the user. For this `POST` method, all the following fields are required in the request body for a successful call:

| Property  | Type   | Description                          |
| --------- | ------ | ------------------------------------ |
| `name`    | String | Name of the camera provider          |
| `brand`   | String | Brand name of the camera provider    |
| `country` | String | Country of origin of camera provider |

A `camera provider` that has been successfully created will return a response with a `"success": true` body and a `200 OK` status. 

### Get a camera provider

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/cameras-providers/{camera_provider_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

> 200 Response

```json
{
  "success": true,
  "data": {
    "name": "GoPro, Inc.",
    "camera_provider_id": "6811b8e899b9e7207775390d9664181b",
    "brand": "GoPro",
    "country": "USA"
  }
}
```

`GET /fleet/camera-providers/{camera_provider_id}`

Get a specific camera provider belonging the company of the user.

<div></div>

### Update a camera provider

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.patch 'https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json'
}

r = requests.patch('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}', params={

}, headers = headers)

print r.json()

```


```shell
curl -X PATCH 'https://api.garuda.io/v2/fleet/cameras-providers/{camera_provider_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "brand": "GoPro (Singapore)",
      "country": "Singapore"
     }'
```


```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "brand": "GoPro (Singapore)",
  "country": "Singapore"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}',
{
  method: 'PATCH',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

> 200 Response

```json
{
  "success": true,
  "data": {
    "name": "GoPro, Inc.",
    "camera_provider_id": "6811b8e899b9e7207775390d9664181b",
    "brand": "GoPro (Singapore)",
    "country": "Singapore"
  }
}
```

`PATCH /fleet/camera-providers/{camera_provider_id}`

Update a specific camera provider belonging the company of the user. For this endpoint, all the fields are optional:

| Property  | Type   | Description                          |
| --------- | ------ | ------------------------------------ |
| `name`    | String | Name of the camera provider          |
| `brand`   | String | Brand name of the camera provider    |
| `country` | String | Country of origin of camera provider |

A camera provider that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status. Response body will also contain the updated `camera_provider` object.

<div></div>

### Delete a camera provider

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X DELETE 'https://api.garuda.io/v2/fleet/cameras-providers/{camera_provider_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```


```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

> 200 Response

```json
{
  "success": true,
  "data": {
    "name": "GoPro, Inc.",
    "camera_provider_id": "6811b8e899b9e7207775390d9664181b",
    "brand": "GoPro",
    "country": "USA"
  }
}
```

`DELETE /fleet/camera-providers/{camera_provider_id}`

Delete a specific camera provider belonging to the company of the user. A valid `camera_provider_id` in the path parameter is required for a successful call.

A successful deletion will return a `200 OK` status and the deleted `camera_provider` object in the response body.

<div></div>