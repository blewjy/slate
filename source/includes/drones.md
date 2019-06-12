## Drones

Fleet APIs allow you to manage your `drones` easily and in an organised manner. You can easily track a lot of different data and information about each drone, using a `drone` object that has the following properties:

| Property      | Type    | Description                                                                               |
| ------------- | ------- | ----------------------------------------------------------------------------------------- |
| `name`        | String  | Name of the drone                                                                         |
| `drone_id`    | String  | Drone ID                                                                                  |
| `model`       | Object  | Object representing the drone model. Contains the `name` of the model and the `model_id`  |
| `notes`       | String  | Descriptive notes for the drone                                                           |
| `acquired_on` | String  | Date that drone was acquired on, in epoch (Unix timestamp), converted to milliseconds     |
| `serviceable` | Boolean | Boolean representing drone's serviceability status *(insert what serviceable means here)* |
| `shared`      | Boolean | Boolean representing drone's shared status. *(insert what shared means here)*             |

### Get all drones

> Code samples

```ruby
require 'rest-client'
require 'json'
headers = {
  'Accept' => 'application/json'
}
result = RestClient.get 'https://api.garuda.io/v2/fleet/drones',
  params: {
  }, headers: headers

p JSON.parse(result)
```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/drones', params={

}, headers = headers)

print r.json()
```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/drones' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```


```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drones',
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
      "name": "DRONE-001",
      "drone_id": "707548a02a1046bd358c54728e5b6156",
      "model": {
        "name": "M400 UAV",
        "model_id": "04e181a4b0dc28898b6f51f9d918bb8e"
      },
      "notes": "Purpose: Security Surveillance",
      "acquired_on": 1554090304172,
      "serviceable": true,
      "shared": false
    },
    {
      "name": "DRONE-002",
      "drone_id": "3a5890b4bae2846f65353992a4b70259",
      "model": {
        "name": "M408 UAV",
        "model_id": "5bb1ef3af490e4e49ad5b369e8b6991f"
      },
      "notes": "Purpose: Plantation",
      "acquired_on": 1554090304172,
      "serviceable": true,
      "shared": false
    }
  ]
}
```

`GET /fleet/drones`

Get all drones belonging to the company of the user. This endpoint returns an array of JSON objects, with each object representing a `drone` in the database.

<div></div>

### Create new drone

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.garuda.io/v2/fleet/drones',
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

r = requests.post('https://api.garuda.io/v2/fleet/drones', params={

}, headers = headers)

print r.json()

```

```shell
curl -X POST 'https://api.garuda.io/v2/fleet/drones' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "name": "DRONE-001",
      "model_id": "04e181a4b0dc28898b6f51f9d918bb8e",
      "notes": "Purpose: Security Surveillance",
      "serviceable": true,
     }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "name": "DRONE-001",
  "model_id": "7e7ed56fed0be0f555f8374e980056cd",
  "notes": "Primary purpose of drone: surveillance",
  "acquired_on": 1554090304172,
  "serviceable": true,
  "shared": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drones',
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
    "name": "DRONE-001",
    "drone_id": "707548a02a1046bd358c54728e5b6156",
    "model": {
      "name": "M400 UAV",
      "model_id": "04e181a4b0dc28898b6f51f9d918bb8e"
    },
    "notes": "Purpose: Security Surveillance",
    "acquired_on": 1554090304172,
    "serviceable": true,
    "shared": false
  }
}
```

`POST /fleet/drones`

Create a new drone belonging to the company of the user. At minimum, you should pass in the following details in the request body:

| Property   | Type   | Description           |
| ---------- | ------ | --------------------- |
| `name`     | String | Name of the drone     |
| `model_id` | String | Model ID of the drone |

`model_id` has to be a valid model ID that already exists in the database.

There are some additional details that you can add to the request body to flesh out your drone details even further:

| Property      | Type    | Description                                                                           |
| ------------- | ------- | ------------------------------------------------------------------------------------- |
| `notes`       | String  | Descriptive notes for the drone                                                       |
| `acquired_on` | String  | Date that drone was acquired on, in epoch (Unix timestamp), converted to milliseconds |
| `serviceable` | Boolean | Boolean representing drone's serviceability status                                    |
| `shared`      | Boolean | Boolean representing drone's shared status.                                           |

A drone that has been successfully created will return a response with a `"success": true` body and a `200 OK` status. 

<div></div>

### Get a drone

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/fleet/drones/{drone_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/drones/{drone_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/drones/{drone_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drones/{drone_id}',
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
    "name": "DRONE-001",
    "drone_id": "707548a02a1046bd358c54728e5b6156",
    "model": {
      "name": "M400 UAV",
      "model_id": "04e181a4b0dc28898b6f51f9d918bb8e"
    },
    "notes": "Purpose: Security Surveillance",
    "acquired_on": 1554090304172,
    "serviceable": true,
    "shared": false
  }
}
```

`GET /fleet/drones/{drone_id}`

Get a specific drone belonging to the company of the user. 

`drone_id` parameter has to be a valid drone ID.

<div></div>

### Update a drone

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.patch 'https://api.garuda.io/v2/fleet/drones/{drone_id}',
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

r = requests.patch('https://api.garuda.io/v2/fleet/drones/{drone_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X PATCH 'https://api.garuda.io/v2/fleet/drones/{drone_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "model_id": "5bb1ef3af490e4e49ad5b369e8b6991f",
      "serviceable": false,
     }'
```


```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "model_id": "5bb1ef3af490e4e49ad5b369e8b6991f",
  "serviceable": false,
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drones/{drone_id}',
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
    "name": "DRONE-001",
    "drone_id": "707548a02a1046bd358c54728e5b6156",
    "model": {
      "name": "M408 UAV",
      "model_id": "5bb1ef3af490e4e49ad5b369e8b6991f"
    },
    "notes": "Purpose: Security Surveillance",
    "acquired_on": 1554090304172,
    "serviceable": false,
    "shared": false
  }
}
```
`PATCH /fleet/drones/{drone_id}`

Update a specific drone belonging to the company of the user.

To update a specific drone, you can pass whichever properties that you wish to update in the request body. All properties are optional.

| Property      | Type    | Description                                                                               |
| ------------- | ------- | ----------------------------------------------------------------------------------------- |
| `name`        | String  | Name of the drone                                                                         |
| `drone_id`    | String  | Drone ID                                                                                  |
| `model`       | Object  | Object representing the drone model. Contains the `name` of the model and the `model_id`  |
| `notes`       | String  | Descriptive notes for the drone                                                           |
| `acquired_on` | String  | Date that drone was acquired on, in epoch (Unix timestamp), converted to milliseconds     |
| `serviceable` | Boolean | Boolean representing drone's serviceability status *(insert what serviceable means here)* |
| `shared`      | Boolean | Boolean representing drone's shared status. *(insert what shared means here)*             |

A drone that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status. Response body will also contain the updated `drone` object.

<div></div>

### Delete a drone

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/fleet/drones/{drone_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/fleet/drones/{drone_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X DELETE 'https://api.garuda.io/v2/fleet/drones/{drone_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```


```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drones/{drone_id}',
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
    "name": "DRONE-001",
    "drone_id": "7e7ed56fed0be0f555f8374e980056cd",
    "model": {
      "name": "M400 UAV",
      "model_id": "7e7ed56fed0be0f555f8374e980056cd"
    },
    "notes": "Primary purpose of drone: surveillance",
    "acquired_on": 1554090304172,
    "serviceable": true,
    "shared": false
  }
}
```

`DELETE /fleet/drones/{drone_id}`

Delete a specific drone belonging to the company of the user. A valid `drone_id` in the path parameter is required for a successful call.

A successful deletion will return a `200 OK` status and the deleted drone object in the response body.

<div></div>