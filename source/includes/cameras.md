## Cameras

You can track and manage your drone cameras using the Cameras API. Each camera is represented by a `camera` object wth the following properties:

| Property      | Type   | Description                                                                               |
| ------------- | ------ | ----------------------------------------------------------------------------------------- |
| `name`        | String | Name of the camera                                                                        |
| `camera_id`   | String | Camera ID                                                                                 |
| `model`       | Object | Object representing the camera model. Contains the `name` of the model and the `model_id` |
| `notes`       | String | Descriptive notes for the camera                                                          |
| `acquired_on` | String | Date that camera was acquired on, in epoch (Unix timestamp), converted to milliseconds    |

### Get all cameras

> Code samples

```ruby
require 'rest-client'
require 'json'
headers = {
  'Accept' => 'application/json'
}
result = RestClient.get 'https://api.garuda.io/v2/fleet/cameras',
  params: {
  }, headers: headers

p JSON.parse(result)
```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/cameras', params={

}, headers = headers)

print r.json()
```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/cameras' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```


```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/cameras',
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
      "name": "CAMERA-001",
      "camera_id": "0b53479856488f542a18fef96b84119d",
      "model": {
        "name": "Powershot S100",
        "model_id": "0e51493cd1ae85c097547de808642659"
      },
      "notes": "For front facing camera",
      "acquired_on": 1554090304172,
    },
    {
      "name": "CAMERA-002",
      "camera_id": "df0fb1aed5215106cf5bd23f8a005a55",
      "model": {
        "name": "Git2",
        "model_id": "f473a293f4294c6890f955fad4d10dc1"
      },
      "notes": "For downward facing camera",
      "acquired_on": 1554090304172,
    }
  ]
}
```

`GET /fleet/cameras`

Get all cameras belonging to the company of the user. This endpoint returns an array of JSON objects, with each object representing a `camera` in the database.

<div></div>

### Create new camera

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.garuda.io/v2/fleet/cameras',
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

r = requests.post('https://api.garuda.io/v2/fleet/cameras', params={

}, headers = headers)

print r.json()

```

```shell
curl -X POST 'https://api.garuda.io/v2/fleet/cameras' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "name": "CAMERA-001",
      "model_id": "0e51493cd1ae85c097547de808642659",
      "notes": "For front facing camera"
     }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "name": "CAMERA-001",
  "model_id": "0e51493cd1ae85c097547de808642659",
  "notes": "For front facing camera"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/cameras',
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
    "name": "CAMERA-001",
    "camera_id": "0b53479856488f542a18fef96b84119d",
    "model": {
      "name": "Powershot S100",
      "model_id": "0e51493cd1ae85c097547de808642659"
    },
    "notes": "For front facing camera",
    "acquired_on": 1554090304172,
  }
}
```

`POST /fleet/cameras`

Create a new camera belonging to the company of the user. At minimum, you should pass in the following details in the request body:

| Property   | Type   | Description            |
| ---------- | ------ | ---------------------- |
| `name`     | String | Name of the camera     |
| `model_id` | String | Model ID of the camera |

`model_id` has to be a valid model ID that already exists in the database.

There are some additional details that you can add to the request body to flesh out your camera details even further:

| Property      | Type   | Description                                                                            |
| ------------- | ------ | -------------------------------------------------------------------------------------- |
| `notes`       | String | Descriptive notes for the camera                                                       |
| `acquired_on` | String | Date that camera was acquired on, in epoch (Unix timestamp), converted to milliseconds |

If the `acquired_on` property is not specified, it will be saved as the time that the request was made.

A camera that has been successfully created will return a response with a `"success": true` body and a `200 OK` status. 

<div></div>

### Get a camera

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/fleet/cameras/{camera_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/cameras/{camera_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/cameras/{camera_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/cameras/{camera_id}',
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
    "name": "CAMERA-001",
    "camera_id": "0b53479856488f542a18fef96b84119d",
    "model": {
      "name": "Powershot S100",
      "model_id": "0e51493cd1ae85c097547de808642659"
    },
    "notes": "For front facing camera",
    "acquired_on": 1554090304172,
  }
}
```

`GET /fleet/cameras/{camera_id}`

Get a specific camera belonging to the company of the user. 

`camera_id` parameter has to be a valid camera ID.

<div></div>

### Update a camera

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.patch 'https://api.garuda.io/v2/fleet/cameras/{camera_id}',
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

r = requests.patch('https://api.garuda.io/v2/fleet/cameras/{camera_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X PATCH 'https://api.garuda.io/v2/fleet/cameras/{camera_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "notes": "For front facing camera, can also be used for downward facing"
     }'
```


```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "notes": "For front facing camera, can also be used for downward facing"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/cameras/{camera_id}',
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
    "name": "CAMERA-001",
    "camera_id": "0b53479856488f542a18fef96b84119d",
    "model": {
      "name": "Powershot S100",
      "model_id": "0e51493cd1ae85c097547de808642659"
    },
    "notes": "For front facing camera, can also be used for downward facing",
    "acquired_on": 1554090304172,
  }
}
```

`PATCH /fleet/cameras/{camera_id}`

Update a specific camera belonging to the company of the user.

To update a specific camera, you can pass whichever properties that you wish to update in the request body. All properties are optional.

| Property      | Type   | Description                                                                               |
| ------------- | ------ | ----------------------------------------------------------------------------------------- |
| `name`        | String | Name of the camera                                                                        |
| `camera_id`   | String | Camera ID                                                                                 |
| `model`       | Object | Object representing the camera model. Contains the `name` of the model and the `model_id` |
| `notes`       | String | Descriptive notes for the camera                                                          |
| `acquired_on` | String | Date that camera was acquired on, in epoch (Unix timestamp), converted to milliseconds    |

A camera that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status. Response body will also contain the updated `camera` object.

<div></div>

### Delete a camera

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/fleet/cameras/{camera_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/fleet/cameras/{camera_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X DELETE 'https://api.garuda.io/v2/fleet/cameras/{camera_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```


```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/cameras/{camera_id}',
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
    "name": "CAMERA-001",
    "camera_id": "0b53479856488f542a18fef96b84119d",
    "model": {
      "name": "Powershot S100",
      "model_id": "0e51493cd1ae85c097547de808642659"
    },
    "notes": "For front facing camera",
    "acquired_on": 1554090304172,
  }
}
```

`DELETE /fleet/cameras/{camera_id}`

Delete a specific camera belonging to the company of the user. A valid `camera_id` in the path parameter is required for a successful call.

A successful deletion will return a `200 OK` status and the deleted camera object in the response body.

<div></div>