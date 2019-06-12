## Batteries

You can track and manage your drone batteries using the batteries API. Each battery is represented by a `battery` object wth the following properties:

| Property      | Type    | Description                                                                                |
| ------------- | ------- | ------------------------------------------------------------------------------------------ |
| `name`        | String  | Name of the battery                                                                        |
| `battery_id`  | String  | Battery ID                                                                                 |
| `model`       | Object  | Object representing the battery model. Contains the `name` of the model and the `model_id` |
| `notes`       | String  | Descriptive notes for the battery                                                          |
| `acquired_on` | String  | Date that battery was acquired on, in epoch (Unix timestamp), converted to milliseconds    |
| `shared`      | Boolean | Boolean representing battery's shared status. *(insert what shared means here)*            |

### Get all batteries

> Code samples

```ruby
require 'rest-client'
require 'json'
headers = {
  'Accept' => 'application/json'
}
result = RestClient.get 'https://api.garuda.io/v2/fleet/batteries',
  params: {
  }, headers: headers

p JSON.parse(result)
```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/batteries', params={

}, headers = headers)

print r.json()
```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/batteries' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```


```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/batteries',
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
      "name": "BATTERY-001",
      "model": {
        "name": "Multistar 6S 6600",
        "model_id": "4b38b7383fdb23fbff8c3a6a694e4533"
      },
      "notes": "This battery is meant for small drones only.",
      "shared": false,
      "acquired_on": 1554090304172
    }
  ]
}
```

`GET /fleet/batteries`

Get all batteries belonging to the company of the user. This endpoint returns an array of JSON objects, with each object representing a `battery` in the database.

<div></div>

### Create new battery

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.garuda.io/v2/fleet/batteries',
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

r = requests.post('https://api.garuda.io/v2/fleet/batteries', params={

}, headers = headers)

print r.json()

```

```shell
curl -X POST 'https://api.garuda.io/v2/fleet/batteries' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "name": "BATTERY-001",
      "model_id": "4b38b7383fdb23fbff8c3a6a694e4533",
      "notes": "This battery is meant for small drones only."
     }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "name": "BATTERY-001",
  "model_id": "4b38b7383fdb23fbff8c3a6a694e4533",
  "notes": "This battery is meant for small drones only."
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/batteries',
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
    "name": "BATTERY-001",
    "model": {
      "name": "Multistar 6S 6600",
      "model_id": "4b38b7383fdb23fbff8c3a6a694e4533"
    },
    "notes": "This battery is meant for small drones only.",
    "shared": false,
    "acquired_on": 1554090304172
  }
}
```

`POST /fleet/batteries`

Create a new battery belonging to the company of the user. At minimum, you should pass in the following details in the request body:

| Property   | Type   | Description             |
| ---------- | ------ | ----------------------- |
| `name`     | String | Name of the battery     |
| `model_id` | String | Model ID of the battery |

`model_id` has to be a valid model ID that already exists in the database.

There are some additional details that you can add to the request body to flesh out your battery details even further:

| Property      | Type    | Description                                                                             |
| ------------- | ------- | --------------------------------------------------------------------------------------- |
| `notes`       | String  | Descriptive notes for the battery                                                       |
| `acquired_on` | String  | Date that battery was acquired on, in epoch (Unix timestamp), converted to milliseconds |
| `shared`      | Boolean | Boolean representing battery's shared status. *(insert what shared means here)*         |

If the `acquired_on` property is not specified, it will be saved as the time that the request was made.

If the `shared` property is not specified, the default value is **false**.

A battery that has been successfully created will return a response with a `"success": true` body and a `200 OK` status. 

<div></div>

### Get a battery

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/fleet/batteries/{battery_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/batteries/{battery_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/batteries/{battery_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/batteries/{battery_id}',
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
    "name": "BATTERY-001",
    "model": {
      "name": "Multistar 6S 6600",
      "model_id": "4b38b7383fdb23fbff8c3a6a694e4533"
    },
    "notes": "This battery is meant for small drones only.",
    "shared": false,
    "acquired_on": 1554090304172
  }
}
```

`GET /fleet/batteries/{battery_id}`

Get a specific battery belonging to the company of the user. 

`battery_id` parameter has to be a valid battery ID.

<div></div>

### Update a battery

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.patch 'https://api.garuda.io/v2/fleet/batteries/{battery_id}',
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

r = requests.patch('https://api.garuda.io/v2/fleet/batteries/{battery_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X PATCH 'https://api.garuda.io/v2/fleet/batteries/{battery_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "notes": "Can be used for both small and large drones"
     }'
```


```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "notes": "Can be used for both small and large drones"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/batteries/{battery_id}',
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
    "name": "BATTERY-001",
    "model": {
      "name": "Multistar 6S 6600",
      "model_id": "4b38b7383fdb23fbff8c3a6a694e4533"
    },
    "notes": "Can be used for both small and large drones",
    "shared": false,
    "acquired_on": 1554090304172
  }
}
```

`PATCH /fleet/batteries/{battery_id}`

Update a specific battery belonging to the company of the user.

To update a specific battery, you can pass whichever properties that you wish to update in the request body. All properties are optional.

| Property      | Type   | Description                                                                                |
| ------------- | ------ | ------------------------------------------------------------------------------------------ |
| `name`        | String | Name of the battery                                                                        |
| `battery_id`  | String | battery ID                                                                                 |
| `model`       | Object | Object representing the battery model. Contains the `name` of the model and the `model_id` |
| `notes`       | String | Descriptive notes for the battery                                                          |
| `acquired_on` | String | Date that battery was acquired on, in epoch (Unix timestamp), converted to milliseconds    |

A battery that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status. Response body will also contain the updated `battery` object.

<div></div>

### Delete a battery

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/fleet/batteries/{battery_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/fleet/batteries/{battery_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X DELETE 'https://api.garuda.io/v2/fleet/batteries/{battery_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```


```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/batteries/{battery_id}',
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
    "name": "BATTERY-001",
    "model": {
      "name": "Multistar 6S 6600",
      "model_id": "4b38b7383fdb23fbff8c3a6a694e4533"
    },
    "notes": "This battery is meant for small drones only.",
    "shared": false,
    "acquired_on": 1554090304172
  }
}
```

`DELETE /fleet/batteries/{battery_id}`

Delete a specific battery belonging to the company of the user. A valid `battery_id` in the path parameter is required for a successful call.

A successful deletion will return a `200 OK` status and the deleted battery object in the response body.

<div></div>