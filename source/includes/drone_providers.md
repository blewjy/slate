
## Drone Providers

Drone providers are companies/brands that supply drones to consumers. The Fleet APIs allow you to manage your company's drone providers, with each `drone_provider` object having the following properties:

| Property            | Type   | Description                         |
| ------------------- | ------ | ----------------------------------- |
| `name`              | String | Name of the drone provider          |
| `drone_provider_id` | String | A unique drone provider ID          |
| `brand`             | String | Brand name of the drone provider    |
| `country`           | String | Country of origin of drone provider |

### Get all drone providers

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/fleet/drone-providers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/drone-providers', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/drone-providers' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drone-providers',
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
      "name": "Garuda Robotics Pte. Ltd.",
      "drone_provider_id": "d2a99141fd4122869b5099138a5124d2",
      "brand": "Garuda",
      "country": "Singapore"
    },
    {
      "name": "Rugada Robotics Pte. Ltd.",
      "drone_provider_id": "fda3963d33db33c5023d33b5e863a19f",
      "brand": "Rugada",
      "country": "Singapore"
    }
  ]
}
```

`GET /fleet/drone-providers`

Get all drones providers belonging to the company of the user. The response returns an array of all the `drone_provider` objects that belong to your company.

<div></div>

### Create new drone provider

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.garuda.io/v2/fleet/drone-providers',
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

r = requests.post('https://api.garuda.io/v2/fleet/drone-providers', params={

}, headers = headers)

print r.json()

```

```shell
curl -X POST 'https://api.garuda.io/v2/fleet/drones-providers' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "name": "Garuda Robotics Pte. Ltd.",
      "brand": "Garuda",
      "country": "Singapore"
     }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "name": "Garuda Robotics Pte. Ltd.",
  "brand": "Garuda",
  "country": "Singapore"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drone-providers',
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
    "name": "Garuda Robotics Pte. Ltd.",
    "drone_provider_id": "d2a99141fd4122869b5099138a5124d2",
    "brand": "Garuda",
    "country": "Singapore"
  }
}
```

`POST /fleet/drone-providers`

Create a new drone provider belonging to the company of the user. For this `POST` method, all the following fields are required in the request body for a successful call:

| Property  | Type   | Description                         |
| --------- | ------ | ----------------------------------- |
| `name`    | String | Name of the drone provider          |
| `brand`   | String | Brand name of the drone provider    |
| `country` | String | Country of origin of drone provider |

A `drone provider` that has been successfully created will return a response with a `"success": true` body and a `200 OK` status. 

### Get a drone provider

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/drones-providers/{drone_provider_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}',
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
    "name": "Garuda Robotics Pte. Ltd.",
    "drone_provider_id": "d2a99141fd4122869b5099138a5124d2",
    "brand": "Garuda",
    "country": "Singapore"
  }
}
```

`GET /fleet/drone-providers/{drone_provider_id}`

Get a specific drone provider belonging the company of the user.

<div></div>

### Update a drone provider

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.patch 'https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}',
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

r = requests.patch('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}', params={

}, headers = headers)

print r.json()

```


```shell
curl -X PATCH 'https://api.garuda.io/v2/fleet/drones-providers/{drone_provider_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "brand": "Garuda Robotics"
     }'
```


```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "brand": "Garuda Robotics"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}',
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
    "name": "Garuda Robotics Pte. Ltd.",
    "drone_provider_id": "d2a99141fd4122869b5099138a5124d2",
    "brand": "Garuda Robotics",
    "country": "Singapore"
  }
}
```

`PATCH /fleet/drone-providers/{drone_provider_id}`

Update a specific drone provider belonging the company of the user. For this endpoint, all the fields are optional:

| Property  | Type   | Description                         |
| --------- | ------ | ----------------------------------- |
| `name`    | String | Name of the drone provider          |
| `brand`   | String | Brand name of the drone provider    |
| `country` | String | Country of origin of drone provider |

A drone provider that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status. Response body will also contain the updated `drone_provider` object.

<div></div>

### Delete a drone provider

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X DELETE 'https://api.garuda.io/v2/fleet/drones-providers/{drone_provider_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```


```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}',
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
    "name": "Garuda Robotics Pte. Ltd.",
    "drone_provider_id": "d2a99141fd4122869b5099138a5124d2",
    "brand": "Garuda",
    "country": "Singapore"
  }
}
```

`DELETE /fleet/drone-providers/{drone_provider_id}`

Delete a specific drone provider belonging to the company of the user. A valid `drone_provider_id` in the path parameter is required for a successful call.

A successful deletion will return a `200 OK` status and the deleted `drone_provider` object in the response body.

<div></div>