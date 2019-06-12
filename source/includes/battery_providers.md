
## Battery Providers

Battery providers are companies/brands that supply batteries to consumers. The Fleet APIs allow you to manage your company's battery providers, with each `battery_provider` object having the following properties:

| Property              | Type   | Description                           |
| --------------------- | ------ | ------------------------------------- |
| `name`                | String | Name of the battery provider          |
| `battery_provider_id` | String | A unique battery provider ID          |
| `brand`               | String | Brand name of the battery provider    |
| `country`             | String | Country of origin of battery provider |

### Get all battery providers

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/fleet/battery-providers',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/battery-providers', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/battery-providers' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/battery-providers',
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
      "name": "Da-Jiang Innovations Science and Technology Co., Ltd",
      "battery_provider_id": "1c9e81a9a3352cd010857331acd63a92",
      "brand": "DJI",
      "country": "China"
    }
  ]
}
```

`GET /fleet/battery-providers`

Get all batteries providers belonging to the company of the user. The response returns an array of all the `battery_provider` objects that belong to your company.

<div></div>

### Create new battery provider

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.garuda.io/v2/fleet/battery-providers',
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

r = requests.post('https://api.garuda.io/v2/fleet/battery-providers', params={

}, headers = headers)

print r.json()

```

```shell
curl -X POST 'https://api.garuda.io/v2/fleet/batteries-providers' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "name": "Da-Jiang Innovations Science and Technology Co., Ltd",
      "brand": "DJI",
      "country": "China"
     }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
 "name": "Da-Jiang Innovations Science and Technology Co., Ltd",
  "brand": "DJI",
  "country": "China"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/battery-providers',
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
    "name": "Da-Jiang Innovations Science and Technology Co., Ltd",
    "battery_provider_id": "1c9e81a9a3352cd010857331acd63a92",
    "brand": "DJI",
    "country": "China"
  }
}
```

`POST /fleet/battery-providers`

Create a new battery provider belonging to the company of the user. For this `POST` method, all the following fields are required in the request body for a successful call:

| Property  | Type   | Description                           |
| --------- | ------ | ------------------------------------- |
| `name`    | String | Name of the battery provider          |
| `brand`   | String | Brand name of the battery provider    |
| `country` | String | Country of origin of battery provider |

A `battery provider` that has been successfully created will return a response with a `"success": true` body and a `200 OK` status. 

### Get a battery provider

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/batteries-providers/{battery_provider_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}',
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
    "name": "Da-Jiang Innovations Science and Technology Co., Ltd",
    "battery_provider_id": "1c9e81a9a3352cd010857331acd63a92",
    "brand": "DJI",
    "country": "China"
  }
}
```

`GET /fleet/battery-providers/{battery_provider_id}`

Get a specific battery provider belonging the company of the user.

<div></div>

### Update a battery provider

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.patch 'https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}',
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

r = requests.patch('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}', params={

}, headers = headers)

print r.json()

```


```shell
curl -X PATCH 'https://api.garuda.io/v2/fleet/batteries-providers/{battery_provider_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "brand": "DJI - China"
     }'
```


```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "brand": "DJI - China"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}',
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
    "name": "Da-Jiang Innovations Science and Technology Co., Ltd",
    "battery_provider_id": "1c9e81a9a3352cd010857331acd63a92",
    "brand": "DJI - China",
    "country": "China"
  }
}
```

`PATCH /fleet/battery-providers/{battery_provider_id}`

Update a specific battery provider belonging the company of the user. For this endpoint, all the fields are optional:

| Property  | Type   | Description                           |
| --------- | ------ | ------------------------------------- |
| `name`    | String | Name of the battery provider          |
| `brand`   | String | Brand name of the battery provider    |
| `country` | String | Country of origin of battery provider |

A battery provider that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status. Response body will also contain the updated `battery_provider` object.

<div></div>

### Delete a battery provider

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X DELETE 'https://api.garuda.io/v2/fleet/batteries-providers/{battery_provider_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```


```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}',
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
    "name": "Da-Jiang Innovations Science and Technology Co., Ltd",
    "battery_provider_id": "1c9e81a9a3352cd010857331acd63a92",
    "brand": "DJI",
    "country": "China"
  }
}
```

`DELETE /fleet/battery-providers/{battery_provider_id}`

Delete a specific battery provider belonging to the company of the user. A valid `battery_provider_id` in the path parameter is required for a successful call.

A successful deletion will return a `200 OK` status and the deleted `battery_provider` object in the response body.

<div></div>