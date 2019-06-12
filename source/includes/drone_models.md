
## Drone Models

Fleet APIs allow you to manage drone models. Each `drone_model` object contains information regarding a specific drone model provided by a drone provider. A `drone_model` object has the following properties:

| Property        | Type   | Description                                                                                                                                                                  |
| --------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`          | String | Name of the drone model                                                                                                                                                      |
| `model_id`      | String | Drone model ID                                                                                                                                                               |
| `provider`      | Object | Object representing the drone provider. Contains the `name` of the provider and the `provider_id`                                                                            |
| `category`      | String | Name of category of drone                                                                                                                                                    |
| `avatar`        | String | Path to the avatar file for the drone model                                                                                                                                  |
| `compatibility` | Object | An object containing two arrays, `batteries` and `cameras`, each containing a list of `battery` and `camera` objects respectively that are compatible with this drone model. |
| `weight`        | String | Weight of the drone in kilograms (kg)                                                                                                                                        |
| `properties`    | Object | Object representing the properties of this drone model. (see below)                                                                                                          |

Each `drone_model` has a set of `properties` that describes the specifications of the drone model. The `properties` in the `drone_model` is an object with the following properties:

| Property          | Type   | Description                                                                        |
| ----------------- | ------ | ---------------------------------------------------------------------------------- |
| `dimensions`      | Object | Dimensions of drone. Object has the properties `width`, `length`, and `height` (m) |
| `max_flight_time` | String | Description of the maximum flight time of the drone                                |
| `rc_frequency`    | String | The RC frequency at which the drone operates at                                    |

### Get all drone models

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models',
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
      "name": "M400 UAV",
      "model_id": "04e181a4b0dc28898b6f51f9d918bb8e",
      "provider": {
        "name": "Garuda Robotics Pte. Ltd.",
        "provider_id": "d2a99141fd4122869b5099138a5124d2"
      },
      "category": "Quadcopter"
    }
  ]
}
```

`GET /fleet/drone-providers/{drone_provider_id}/drone-models`

When getting all `drone_models` belonging to a specific drone provider in your company, you have to provide a valid and existing `drone_provider_id`. The HTTP response body will contain an array of `drone_model` objects belonging to your specified `drone_provider`.

You can specify the extent of which to fetch the data via query strings:

| Query     | Default   | Values            | Description                                                 |
| --------- | --------- | ----------------- | ----------------------------------------------------------- |
| `options` | `shallow` | `shallow`, `deep` | Specify if data retrieved should be a deep or shallow fetch |

For a `shallow` fetch (which is the default behaviour), only the `name`, `provider`, `avatar` and `category` will be retrieved (see sample response on the left for how this will look like). A `deep` fetch will retrieve more information for each of the objects -- to see the exact properties that will be retrieved with a `deep` fetch, refer to the [beginning of this section](#drone-models).

<div></div>

### Create new drone model

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models',
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

r = requests.post('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models', params={

}, headers = headers)

print r.json()

```

```shell
curl -X POST 'https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "name": "M400 UAV",
      "provider_id": "d2a99141fd4122869b5099138a5124d2",
      "category": "Quadcopter",
      "weight": 2.8,
      "properties": {
        "dimensions": {
          "width": "1.30",
          "length": "1.30",
          "height": "0.30"
        },
        "max_flight_time": "26 mins",
        "rc_frequency": "2.400GHz"
      }
     }'
```


```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "name": "M400 UAV",
  "provider_id": "d2a99141fd4122869b5099138a5124d2",
  "category": "Quadcopter",
  "weight": 2.8,
  "properties": {
    "dimensions": {
      "width": "1.30",
      "length": "1.30",
      "height": "0.30"
    },
    "max_flight_time": "26 mins",
    "rc_frequency": "2.400GHz"
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models',
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
    "name": "M400 UAV",
    "provider": {
      "name": "Garuda Robotics Pte. Ltd.",
      "provider_id": "d2a99141fd4122869b5099138a5124d2",
    },
    "category": "Quadcopter",
    "weight": 2.8,
    "properties": {
      "dimensions": {
        "width": "1.30",
        "length": "1.30",
        "height": "0.30"
      },
      "max_flight_time": "26 mins",
      "rc_frequency": "2.400GHz"
    }
  }
}
```


`POST /fleet/drone-providers/{drone_provider_id}/drone-models`

Every created `drone_model` has to belong to a valid and existing `drone_provider`. When calling this API, the `drone_provider_id` parameter has to be valid for a successful call.

When creating a new `drone_model`, at minimum, you should pass in values for the following properties:

| Property     | Type   | Description                                                                                       |
| ------------ | ------ | ------------------------------------------------------------------------------------------------- |
| `name`       | String | Name of the drone model                                                                           |
| `model_id`   | String | Drone model ID                                                                                    |
| `provider`   | Object | Object representing the drone provider. Contains the `name` of the provider and the `provider_id` |
| `category`   | String | Name of category of drone                                                                         |
| `avatar`     | String | Path to the avatar file for the drone model                                                       |
| `weight`     | String | Weight of the drone in kilograms (kg)                                                             |
| `properties` | Object | Object representing the properties of this drone model. (see below)                               |

For more information on these properties, refer to the `drone_model` object description at the [beginning of this section](#drone-models)

You can also choose to pass in equipment `compatibility` information if you wish.

| Property        | Type   | Description                                                                                                                                                                  |
| --------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `compatibility` | Object | An object containing two arrays, `batteries` and `cameras`, each containing a list of `battery` and `camera` objects respectively that are compatible with this drone model. |

Otherwise, `compatibility` can also be added at a later time with the [`PATCH` endpoint](#update-a-drone-model).

<div></div>

### Update a drone model

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.patch 'https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models/{drone_model_id}',
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

r = requests.patch('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models/{drone_model_id}', params={

}, headers = headers)

print r.json()

```


```shell
curl -X PATCH 'https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models/{drone_model_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "compatibility": {
        "batteries": [
          {
            "name": "BATTERY-001",
            "battery_id": "f42074ff0948fbb1d11f7a96c07cdcdd",
            "model_name": "Multistar 6S 6600",
          }
        ],
        "cameras": [
          {
            "name": "CAMERA-001",
            "camera_id": "0b53479856488f542a18fef96b84119d",
            "model_name": "Powershot S100",
          }
        ]
      }
     }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "compatibility": {
    "batteries": [
      {
        "name": "BATTERY-001",
        "battery_id": "f42074ff0948fbb1d11f7a96c07cdcdd",
        "model_name": "Multistar 6S 6600",
      }
    ],
    "cameras": [
      {
        "name": "CAMERA-001",
        "camera_id": "0b53479856488f542a18fef96b84119d",
        "model_name": "Powershot S100",
      }
    ]
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models/{drone_model_id}',
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
    "name": "M400 UAV",
    "provider": {
      "name": "Garuda Robotics Pte. Ltd.",
      "provider_id": "d2a99141fd4122869b5099138a5124d2",
    },
    "category": "Quadcopter",
    "weight": 2.8,
    "compatibility": {
      "batteries": [
        {
          "name": "BATTERY-001",
          "battery_id": "f42074ff0948fbb1d11f7a96c07cdcdd",
          "model_name": "Multistar 6S 6600",
        }
      ],
      "cameras": [
        {
          "name": "CAMERA-001",
          "camera_id": "0b53479856488f542a18fef96b84119d",
          "model_name": "Powershot S100",
        }
      ]
    },
    "properties": {
      "dimensions": {
        "width": "1.30",
        "length": "1.30",
        "height": "0.30"
      },
      "max_flight_time": "26 mins",
      "rc_frequency": "2.400GHz"
    }
  }
}
```

`PATCH /fleet/drone-providers/{drone_provider_id}/drone-models/{drone_model_id}`

This endpoint allows you to edit and update information regarding a `drone_model` that has already been created. For the request body of this endpoint, it is not necessary to pass in values for all the properties of a `drone_model`. All of the following properties are optional: 

| Property        | Type   | Description                                                                                                                                                                  |
| --------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`          | String | Name of the drone model                                                                                                                                                      |
| `model_id`      | String | Drone model ID                                                                                                                                                               |
| `provider`      | Object | Object representing the drone provider. Contains the `name` of the provider and the `provider_id`                                                                            |
| `category`      | String | Name of category of drone                                                                                                                                                    |
| `avatar`        | String | Path to the avatar file for the drone model                                                                                                                                  |
| `compatibility` | Object | An object containing two arrays, `batteries` and `cameras`, each containing a list of `battery` and `camera` objects respectively that are compatible with this drone model. |
| `weight`        | String | Weight of the drone in kilograms (kg)                                                                                                                                        |
| `properties`    | Object | Object representing the properties of this drone model. (see below)                                                                                                          |
For more information on these properties, refer to the `drone_model` object description at the [beginning of this section](#drone-models)

A `drone_model` that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status. Response body will also contain the updated `drone_model` object.

<div></div>

### Delete a drone model

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models/{drone_model_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models/{drone_model_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X DELETE 'https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models/{drone_model_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/drone-providers/{drone_provider_id}/drone-models/{drone_model_id}',
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
    "name": "M400 UAV",
    "provider": {
      "name": "Garuda Robotics Pte. Ltd.",
      "provider_id": "d2a99141fd4122869b5099138a5124d2",
    },
    "category": "Quadcopter",
    "weight": 2.8,
    "compatibility": {
      "batteries": [
        {
          "name": "BATTERY-001",
          "battery_id": "f42074ff0948fbb1d11f7a96c07cdcdd",
          "model_name": "Multistar 6S 6600",
        }
      ],
      "cameras": [
        {
          "name": "CAMERA-001",
          "camera_id": "0b53479856488f542a18fef96b84119d",
          "model_name": "Powershot S100",
        }
      ]
    },
    "properties": {
      "dimensions": {
        "width": "1.30",
        "length": "1.30",
        "height": "0.30"
      },
      "max_flight_time": "26 mins",
      "rc_frequency": "2.400GHz"
    }
  }
}
```

`DELETE /fleet/drone-providers/{drone_provider_id}/drone-models/{drone_model_id}`

Delete a specific drone model of a specific drone provider belonging to the company of the user.
