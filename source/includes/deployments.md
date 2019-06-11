## Deployments

Every time pilots are activated to fly drones, it is known as a `deployment`. A `deployment` is part of larger `project`, typically spans at least 1 flight session (or maybe a few minutes to a few hours), or multiple flight sessions. For each `deployment`, a leader, known as the `deployment lead` will plan the deployment for success, enlisting `pilots`, `drones`, and other equipment necessary. Proper `risk management` is required for every deployment, as are `permits` by the relevant authority (such as an Activity Permit by CAAS). Insurance coverage might also be purchased on a `deployment` basis instead of annual basis.

Each `deployment` object will have the following properties:

| Property          | Type   | Description                                                                                                        |
| ----------------- | ------ | ------------------------------------------------------------------------------------------------------------------ |
| `name`            | String | Name of the deployment                                                                                             |
| `deployment_id`   | String | Unique deployment ID                                                                                               |
| `drones`          | Array  | Array of [drone objects](#) tagged to the deployment                                                               |
| `batteries`       | Array  | Array of [battery objects](#) tagged to the deployment                                                             |
| `cameras`         | Array  | Array of [camera objects](#) tagged to the deployment                                                              |
| `personnel`       | Array  | Array of [user objects](#) representing the personnel involved in the deployment                                   |
| `deployment_lead` | Object | [User object](#) representing the deployment lead                                                                  |
| `purpose`         | Array  | Array of enumerated strings describing the purpose of the deployment. Refer to the table below for the valid enums |
| `start_date`      | String | Start date of deployment in epoch (Unix timestamp), converted to milliseconds (ms)                                 |
| `end_date`        | String | End date of deployment in epoch (Unix timestamp), converted to milliseconds (ms)                                   |
| `deployment_area` | String | [GeoJSON](https://geojson.org) string representation of the deployment area                                        |

The property `purpose` in a each `deployment` is represented by a set of enumerations. When creating a new `deployment`, you should specify one or more of the following `purposes` as an array of strings:

| Purpose                           | 
| --------------------------------- | 
| `Aerial Photography`, `Demonstration`, `Inspection (Building, Facility)`, `Surveillance (Security)`, `First Response`, `Recreational, Internal Training`, `Research & Development`, `Aerial Videography`, `Training (Academy)`, `Survey (Land, Plantation)`, `Delivery, Discharge` |

### Get all deployments


> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/flight/deployments',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/flight/deployments', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/flight/deployments' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments',
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

> Successful call returns a 200 OK response:

```json
{
  "success": true,
  "data": [
    {
      "name": "DEPLOYMENT-001",
      "deployment_id": "9703889c2bb4322025815ed1a0509eba",
      "drones": [
        {
          "name": "DRONE-001",
          "drone_id": "ceaf7e6dc205b365e156bf4f86930408",
          "model_name": "M400 UAV",
          "model_id": "7bd6798cdb0dcb26ca6d3c0ca9c2ae79"
        }
      ],
      "batteries": [
        {
          "name": "BATTERY-001",
          "battery_id": "f42074ff0948fbb1d11f7a96c07cdcdd",
          "model_name": "Multistar 6S 6600",
          "model_id": "4b38b7383fdb23fbff8c3a6a694e4533"
        }
      ],
      "cameras": [
        {
          "name": "CAMERA-001",
          "camera_id": "0b53479856488f542a18fef96b84119d",
          "model_name": "Powershot S100",
          "model_id": "0e51493cd1ae85c097547de808642659"
        }
      ],
      "personnel": [
        {
          "name": "USER-002",
          "user_id": "53494af9b7e38f5df3447d17fe0b7547"
        }
      ],
      "lead": {
        "name": "USER-001",
        "user_id": "3b20c067ab91da9436ddaea6b83a9536"
      },
      "purpose": [
        "Aerial Photography"
      ],
      "start_date": "1559571926000",
      "end_date": "1559572026000",
      "geo_json": "{ \"type\": \"Polygon\", \"coordinates\": [ [ [ -118.37099075317383, 33.85505651142062 ], [ -118.37305068969727, 33.85502978214579 ], [ -118.37347984313963, 33.854673391015496 ], [ -118.37306141853333, 33.85231226221667 ], [ -118.37193489074707, 33.85174201755203 ], [ -118.36997151374815, 33.85176874785573 ], [ -118.36995005607605, 33.8528112231754 ], [ -118.37099075317383, 33.85505651142062 ] ] ] }"
    }
  ]
}
```

`GET /flight/deployments`

Get all deployments belonging to the company of the user. Calling this endpoint will return you an array of JSON objects representing each deployment created under the company.

You can specify the extent of which to fetch the data via query strings:

| Query     | Default   | Values            | Description                                                 |
| --------- | --------- | ----------------- | ----------------------------------------------------------- |
| `options` | `shallow` | `shallow`, `deep` | Specify if data retrieved should be a deep or shallow fetch |

For a `shallow` fetch (which is the default behaviour), the `drones`, `batteries`, `cameras` and `personnel` will be retrieved with only their `name`, `id`, `model_name` and `model_id` (see sample response on the left for how this will look like). A `deep` fetch will retrieve more information for each of the objects -- to see the exact properties that will be retrieved with a `deep` fetch, refer to the [Fleet API](#).

<div></div>

### Create new deployment

> Code samples

```ruby
require 'rest-client'
require 'json'
headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}
result = RestClient.post 'https://api.garuda.io/v2/flight/deployments',
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

r = requests.post('https://api.garuda.io/v2/flight/deployments', params={

}, headers = headers)

print r.json()

```

```shell
curl -X POST 'https://api.garuda.io/v2/flight/deployments' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "name": "DEPLOYMENT-001",
      "drones": [
        "ceaf7e6dc205b365e156bf4f86930408"
      ],
      "batteries": [
        "f42074ff0948fbb1d11f7a96c07cdcdd"
      ],
      "cameras": [
        "0b53479856488f542a18fef96b84119d"
      ],
      "personnel": [
        "53494af9b7e38f5df3447d17fe0b7547"
      ],
      "lead": "3b20c067ab91da9436ddaea6b83a9536",
      "purpose": [
        "Aerial Photography",
      ],
      "start_date": "1559571926000",
      "end_date": "1559572026000",
      "geo_json": "{ \"type\": \"Polygon\", \"coordinates\": [ [ [ -118.37099075317383, 33.85505651142062 ], [ -118.37305068969727, 33.85502978214579 ], [ -118.37347984313963, 33.854673391015496 ], [ -118.37306141853333, 33.85231226221667 ], [ -118.37193489074707, 33.85174201755203 ], [ -118.36997151374815, 33.85176874785573 ], [ -118.36995005607605, 33.8528112231754 ], [ -118.37099075317383, 33.85505651142062 ] ] ] }"
     }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "name": "DEPLOYMENT-001",
  "drones": [
    "ceaf7e6dc205b365e156bf4f86930408"
  ],
  "batteries": [
    "f42074ff0948fbb1d11f7a96c07cdcdd"
  ],
  "cameras": [
    "0b53479856488f542a18fef96b84119d"
  ],
  "personnel": [
    "53494af9b7e38f5df3447d17fe0b7547"
  ],
  "lead": "3b20c067ab91da9436ddaea6b83a9536",
  "purpose": [
    "Aerial Photography",
  ],
  "start_date": "1559571926000",
  "end_date": "1559572026000",
  "geo_json": "{ \"type\": \"Polygon\", \"coordinates\": [ [ [ -118.37099075317383, 33.85505651142062 ], [ -118.37305068969727, 33.85502978214579 ], [ -118.37347984313963, 33.854673391015496 ], [ -118.37306141853333, 33.85231226221667 ], [ -118.37193489074707, 33.85174201755203 ], [ -118.36997151374815, 33.85176874785573 ], [ -118.36995005607605, 33.8528112231754 ], [ -118.37099075317383, 33.85505651142062 ] ] ] }"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments',
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

> Successful call returns a 200 OK response:

```json
{
  "success": true,
  "data": {
    "name": "DEPLOYMENT-001",
    "deployment_id": "9703889c2bb4322025815ed1a0509eba",
    "drones": [
      {
        "name": "DRONE-001",
        "drone_id": "ceaf7e6dc205b365e156bf4f86930408",
        "model_name": "M400 UAV",
        "model_id": "7bd6798cdb0dcb26ca6d3c0ca9c2ae79"
      }
    ],
    "batteries": [
      {
        "name": "BATTERY-001",
        "battery_id": "f42074ff0948fbb1d11f7a96c07cdcdd",
        "model_name": "Multistar 6S 6600",
        "model_id": "4b38b7383fdb23fbff8c3a6a694e4533"
      }
    ],
    "cameras": [
      {
        "name": "CAMERA-001",
        "camera_id": "0b53479856488f542a18fef96b84119d",
        "model_name": "Powershot S100",
        "model_id": "0e51493cd1ae85c097547de808642659"
      }
    ],
    "personnel": [
      {
        "name": "USER-002",
        "user_id": "53494af9b7e38f5df3447d17fe0b7547"
      }
    ],
    "lead": {
      "name": "USER-001",
      "user_id": "3b20c067ab91da9436ddaea6b83a9536"
    },
    "purpose": [
      "Aerial Photography"
    ],
    "start_date": "1559571926000",
    "end_date": "1559572026000",
    "geo_json": "{ \"type\": \"Polygon\", \"coordinates\": [ [ [ -118.37099075317383, 33.85505651142062 ], [ -118.37305068969727, 33.85502978214579 ], [ -118.37347984313963, 33.854673391015496 ], [ -118.37306141853333, 33.85231226221667 ], [ -118.37193489074707, 33.85174201755203 ], [ -118.36997151374815, 33.85176874785573 ], [ -118.36995005607605, 33.8528112231754 ], [ -118.37099075317383, 33.85505651142062 ] ] ] }"
  }
}
```

`POST /flight/deployments`

Create a new deployment belonging to the company of the user. At minimum, you should pass in the following details in the request body:

| Property             | Type   | Description                                                                        |
| -------------------- | ------ | ---------------------------------------------------------------------------------- |
| `name`               | String | Name of the deployment                                                             |
| `drones`             | Array  | Array of drone IDs to be used for the deployment                                   |
| `deployment_lead_id` | String | User ID of the deployment lead                                                     |
| `start_date`         | String | Start date of deployment in epoch (Unix timestamp), converted to milliseconds (ms) |
| `end_date`           | String | End date of deployment in epoch (Unix timestamp), converted to milliseconds (ms)   |
| `deployment_area`    | String | GeoJSON string representation of the deployment area                               |

Note that the drone IDs and user IDs have to be valid. Refer to the [Fleet API](#) for information on how you can create users and drones for your company.

There are some additional details that you can add to the request body to flesh out your deployment details even further:

| Property    | Type  | Description                                                            |
| ----------- | ----- | ---------------------------------------------------------------------- |
| `batteries` | Array | Array of battery IDs to be used for the deployment                     |
| `cameras`   | Array | Array of camera IDs to be used for the deployment                      |
| `personnel` | Array | Array of user IDs of the personnel involved in the deployment          |
| `purpose`   | Array | Array of [enumerated strings of purposes](#deployments) of deployment. |

> *Instead of only passing in IDs, we can support passing in entire objects as well (i.e. entire drone objects, entire camera objects, etc.). Passing in the entire object will automatically create the drone for the user in the backend in addition to creating the deployment as well. This is NOT supported as of now.*


A deployment that has been successfully created will return a response with a `"success": true` body and a `200 OK` status. 

<div></div>

### Get a deployment

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/flight/deployments/{deployment_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/flight/deployments/{deployment_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/flight/deployments/{deployment_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}',
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
      "name": "DEPLOYMENT-001",
      "deployment_id": "9703889c2bb4322025815ed1a0509eba",
      "drones": [
        {
          "name": "DRONE-001",
          "drone_id": "ceaf7e6dc205b365e156bf4f86930408",
          "model_name": "M400 UAV",
          "model_id": "7bd6798cdb0dcb26ca6d3c0ca9c2ae79"
        }
      ],
      "batteries": [
        {
          "name": "BATTERY-001",
          "battery_id": "f42074ff0948fbb1d11f7a96c07cdcdd",
          "model_name": "Multistar 6S 6600",
          "model_id": "4b38b7383fdb23fbff8c3a6a694e4533"
        }
      ],
      "cameras": [
        {
          "name": "CAMERA-001",
          "camera_id": "0b53479856488f542a18fef96b84119d",
          "model_name": "Powershot S100",
          "model_id": "0e51493cd1ae85c097547de808642659"
        }
      ],
      "personnel": [
        {
          "name": "USER-002",
          "user_id": "53494af9b7e38f5df3447d17fe0b7547"
        }
      ],
      "lead": {
        "name": "USER-001",
        "user_id": "3b20c067ab91da9436ddaea6b83a9536"
      },
      "purpose": [
        "Aerial Photography"
      ],
      "start_date": "1559571926000",
      "end_date": "1559572026000",
      "geo_json": "{ \"type\": \"Polygon\", \"coordinates\": [ [ [ -118.37099075317383, 33.85505651142062 ], [ -118.37305068969727, 33.85502978214579 ], [ -118.37347984313963, 33.854673391015496 ], [ -118.37306141853333, 33.85231226221667 ], [ -118.37193489074707, 33.85174201755203 ], [ -118.36997151374815, 33.85176874785573 ], [ -118.36995005607605, 33.8528112231754 ], [ -118.37099075317383, 33.85505651142062 ] ] ] }"
    }
  ]
}
```

`GET /flight/deployments/{deployment_id}`

Get a specific deployment belonging to the company of the user. A valid `deployment_id` in the path parameter is required for a successful call.

The `deployment` object returned will be the complete deployment object (i.e. `deep` fetch).

<div></div>

### Update a deployment

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.patch 'https://api.garuda.io/v2/flight/deployments/{deployment_id}',
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

r = requests.patch('https://api.garuda.io/v2/flight/deployments/{deployment_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X PATCH 'https://api.garuda.io/v2/flight/deployments/{deployment_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
       "purpose": [
         "Demonstration",
         "Training (Academy)"
       ]
     }'
```


```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "purpose": [
    "Demonstration",
    "Training (Academy)"
  ]
}';

const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}',
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
    "name": "DEPLOYMENT-001",
    "deployment_id": "9703889c2bb4322025815ed1a0509eba",
    "drones": [
      {
        "name": "DRONE-001",
        "drone_id": "ceaf7e6dc205b365e156bf4f86930408",
        "model_name": "M400 UAV",
        "model_id": "7bd6798cdb0dcb26ca6d3c0ca9c2ae79"
      }
    ],
    "batteries": [
      {
        "name": "BATTERY-001",
        "battery_id": "f42074ff0948fbb1d11f7a96c07cdcdd",
        "model_name": "Multistar 6S 6600",
        "model_id": "4b38b7383fdb23fbff8c3a6a694e4533"
      }
    ],
    "cameras": [
      {
        "name": "CAMERA-001",
        "camera_id": "0b53479856488f542a18fef96b84119d",
        "model_name": "Powershot S100",
        "model_id": "0e51493cd1ae85c097547de808642659"
      }
    ],
    "personnel": [
      {
        "name": "USER-002",
        "user_id": "53494af9b7e38f5df3447d17fe0b7547"
      }
    ],
    "lead": {
      "name": "USER-001",
      "user_id": "3b20c067ab91da9436ddaea6b83a9536"
    },
    "purpose": [
      "Demonstration",
      "Training (Academy)"
    ],
    "start_date": "1559571926000",
    "end_date": "1559572026000",
    "geo_json": "{ \"type\": \"Polygon\", \"coordinates\": [ [ [ -118.37099075317383, 33.85505651142062 ], [ -118.37305068969727, 33.85502978214579 ], [ -118.37347984313963, 33.854673391015496 ], [ -118.37306141853333, 33.85231226221667 ], [ -118.37193489074707, 33.85174201755203 ], [ -118.36997151374815, 33.85176874785573 ], [ -118.36995005607605, 33.8528112231754 ], [ -118.37099075317383, 33.85505651142062 ] ] ] }"
  }
}
```

`PATCH /flight/deployments/{deployment_id}`

Update a specific deployment belonging to the company of the user.

To update a specific deployment, you can pass whichever properties that you wish to update in the request body. All properties are optional.

| Property             | Type   | Description                                                                        |
| -------------------- | ------ | ---------------------------------------------------------------------------------- |
| `name`               | String | Name of the deployment                                                             |
| `drones`             | Array  | Array of drone IDs to be used for the deployment                                   |
| `deployment_lead_id` | String | User ID of the deployment lead                                                     |
| `start_date`         | String | Start date of deployment in epoch (Unix timestamp), converted to milliseconds (ms) |
| `end_date`           | String | End date of deployment in epoch (Unix timestamp), converted to milliseconds (ms)   |
| `deployment_area`    | String | GeoJSON string representation of the deployment area                               |
| `batteries`          | Array  | Array of battery IDs to be used for the deployment                                 |
| `cameras`            | Array  | Array of camera IDs to be used for the deployment                                  |
| `personnel`          | Array  | Array of user IDs of the personnel involved in the deployment                      |
| `purpose`            | String | Description of the purpose of deployment                                           |

A deployment that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status. Response body will also contain the updated `deployment` object.

<div></div>

### Delete a deployment

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/flight/deployments/{deployment_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/flight/deployments/{deployment_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X DELETE 'https://api.garuda.io/v2/flight/deployments/{deployment_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}',
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
    "name": "DEPLOYMENT-001",
    "deployment_id": "9703889c2bb4322025815ed1a0509eba",
    "drones": [
      {
        "name": "DRONE-001",
        "drone_id": "ceaf7e6dc205b365e156bf4f86930408",
        "model_name": "M400 UAV",
        "model_id": "7bd6798cdb0dcb26ca6d3c0ca9c2ae79"
      }
    ],
    "batteries": [
      {
        "name": "BATTERY-001",
        "battery_id": "f42074ff0948fbb1d11f7a96c07cdcdd",
        "model_name": "Multistar 6S 6600",
        "model_id": "4b38b7383fdb23fbff8c3a6a694e4533"
      }
    ],
    "cameras": [
      {
        "name": "CAMERA-001",
        "camera_id": "0b53479856488f542a18fef96b84119d",
        "model_name": "Powershot S100",
        "model_id": "0e51493cd1ae85c097547de808642659"
      }
    ],
    "personnel": [
      {
        "name": "USER-002",
        "user_id": "53494af9b7e38f5df3447d17fe0b7547"
      }
    ],
    "lead": {
      "name": "USER-001",
      "user_id": "3b20c067ab91da9436ddaea6b83a9536"
    },
    "purpose": [
      "Aerial Photography"
    ],
    "start_date": "1559571926000",
    "end_date": "1559572026000",
    "geo_json": "{ \"type\": \"Polygon\", \"coordinates\": [ [ [ -118.37099075317383, 33.85505651142062 ], [ -118.37305068969727, 33.85502978214579 ], [ -118.37347984313963, 33.854673391015496 ], [ -118.37306141853333, 33.85231226221667 ], [ -118.37193489074707, 33.85174201755203 ], [ -118.36997151374815, 33.85176874785573 ], [ -118.36995005607605, 33.8528112231754 ], [ -118.37099075317383, 33.85505651142062 ] ] ] }"
  }
}
```

`DELETE /flight/deployments/{deployment_id}`

Delete a specific deployment belonging to the company of the user. A valid `deployment_id` in the path parameter is required for a successful call.

A successful deletion will return a `200 OK` status and the deleted deployment object in the response body.

<div></div>