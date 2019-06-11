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

```http
GET https://api.garuda.io/v2/flight/deployments HTTP/1.1
Host: api.garuda.io/v2
Accept: application/json
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
      "name": "Zhao Shi Chong's Deployment on 2018-05-22",
      "deployment_id": "0c5c21b6a42fadb018a5d1863c312345",
      "drones": [
        {
          "name": "DEV-001",
          "drone_id": "0c5c21b6a42fadb018a5d1863c312345",
          "model_name": "M400 UAV",
          "model_id": "0c5c21b6a42fadb018a5d1863c312345"
        }
      ],
      "batteries": [
        {
          "name": "BATTERY-001",
          "battery_id": "0c5c21b6a42fadb018a5d1863c312345",
          "model_name": "Multistar 6S 6600",
          "model_id": "0c5c21b6a42fadb018a5d1863c312345"
        }
      ],
      "cameras": [
        {
          "name": "CAMERA-001",
          "camera_id": "0c5c21b6a42fadb018a5d1863c312345",
          "model_name": "Huawei P30 Pro",
          "model_id": "0c5c21b6a42fadb018a5d1863c312345"
        }
      ],
      "personnel": [
        {
          "name": "Jayson Beltran",
          "user_id": "0c5c21b6a42fadb018a5d1863c312345"
        }
      ],
      "lead": {
        "name": "Asher Solomon",
        "user_id": "0c5c21b6a42fadb018a5d1863c312345"
      },
      "purpose": [
        "Photography",
        "Analytics",
        "Security checks"
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

```http
POST https://api.garuda.io/v2/flight/deployments HTTP/1.1
Host: api.garuda.io/v2
Content-Type: application/json
Accept: application/json
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "name": "Zhao Shi Chong's Deployment on 2018-05-22",
  "drones": [
    "0c5c21b6a42fadb018a5d1863c312345",
    "0c5c21b6a42fadb018a5d1863c312345"
  ],
  "batteries": [
    "0c5c21b6a42fadb018a5d1863c312345",
    "0c5c21b6a42fadb018a5d1863c312345"
  ],
  "cameras": [
    "0c5c21b6a42fadb018a5d1863c312345",
    "0c5c21b6a42fadb018a5d1863c312345"
  ],
  "personnel": [
    "0c5c21b6a42fadb018a5d1863c312345",
    "0c5c21b6a42fadb018a5d1863c312345"
  ],
  "lead": "0c5c21b6a42fadb018a5d1863c312345",
  "purpose": [
    "Photography",
    "Analytics",
    "Security checks"
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
    "name": "Zhao Shi Chong's Deployment on 2018-05-22",
    "deployment_id": "0c5c21b6a42fadb018a5d1863c312345",
    "drones": [
      {
        "name": "DEV-001",
        "drone_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "M400 UAV",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      }
    ],
    "batteries": [
      {
        "name": "BATTERY-001",
        "battery_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "Multistar 6S 6600",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      }
    ],
    "cameras": [
      {
        "name": "CAMERA-001",
        "camera_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "Huawei P30 Pro",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      }
    ],
    "personnel": [
      {
        "name": "Jayson Beltran",
        "user_id": "0c5c21b6a42fadb018a5d1863c312345"
      }
    ],
    "lead": {
      "name": "Asher Solomon",
      "user_id": "0c5c21b6a42fadb018a5d1863c312345"
    },
    "purpose": [
      "Photography",
      "Analytics",
      "Security checks"
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

```http
GET https://api.garuda.io/v2/flight/deployments/{deployment_id} HTTP/1.1
Host: api.garuda.io/v2
Accept: application/json

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
      "name": "Zhao Shi Chong's Deployment on 2018-05-22",
      "deployment_id": "0c5c21b6a42fadb018a5d1863c312345",
      "drones": [
        {
          "name": "DEV-001",
          "drone_id": "0c5c21b6a42fadb018a5d1863c312345",
          "model_name": "M400 UAV",
          "model_id": "0c5c21b6a42fadb018a5d1863c312345"
        }
      ],
      "batteries": [
        {
          "name": "BATTERY-001",
          "battery_id": "0c5c21b6a42fadb018a5d1863c312345",
          "model_name": "Multistar 6S 6600",
          "model_id": "0c5c21b6a42fadb018a5d1863c312345"
        }
      ],
      "cameras": [
        {
          "name": "CAMERA-001",
          "camera_id": "0c5c21b6a42fadb018a5d1863c312345",
          "model_name": "Huawei P30 Pro",
          "model_id": "0c5c21b6a42fadb018a5d1863c312345"
        }
      ],
      "personnel": [
        {
          "name": "Jayson Beltran",
          "user_id": "0c5c21b6a42fadb018a5d1863c312345"
        }
      ],
      "lead": {
        "name": "Asher Solomon",
        "user_id": "0c5c21b6a42fadb018a5d1863c312345"
      },
      "purpose": [
        "Photography",
        "Analytics",
        "Security checks"
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

```http
PATCH https://api.garuda.io/v2/flight/deployments/{deployment_id} HTTP/1.1
Host: api.garuda.io/v2
Content-Type: application/json
Accept: application/json

```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "name": "Zhao Shi Chong's Deployment on 2018-05-22",
  "drones": [
    "0c5c21b6a42fadb018a5d1863c312345",
    "0c5c21b6a42fadb018a5d1863c312345"
  ],
  "batteries": [
    "0c5c21b6a42fadb018a5d1863c312345",
    "0c5c21b6a42fadb018a5d1863c312345"
  ],
  "cameras": [
    "0c5c21b6a42fadb018a5d1863c312345",
    "0c5c21b6a42fadb018a5d1863c312345"
  ],
  "personnel": [
    "0c5c21b6a42fadb018a5d1863c312345",
    "0c5c21b6a42fadb018a5d1863c312345"
  ],
  "lead": "0c5c21b6a42fadb018a5d1863c312345",
  "purpose": [
    "Photography",
    "Analytics",
    "Security checks"
  ],
  "start_date": "1559571926000",
  "end_date": "1559572026000",
  "geo_json": "{ \"type\": \"Polygon\", \"coordinates\": [ [ [ -118.37099075317383, 33.85505651142062 ], [ -118.37305068969727, 33.85502978214579 ], [ -118.37347984313963, 33.854673391015496 ], [ -118.37306141853333, 33.85231226221667 ], [ -118.37193489074707, 33.85174201755203 ], [ -118.36997151374815, 33.85176874785573 ], [ -118.36995005607605, 33.8528112231754 ], [ -118.37099075317383, 33.85505651142062 ] ] ] }"
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
    "name": "Zhao Shi Chong's Deployment on 2018-05-22",
    "deployment_id": "0c5c21b6a42fadb018a5d1863c312345",
    "drones": [
      {
        "name": "DEV-001",
        "drone_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "M400 UAV",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      },
      {
        "name": "DEV-002",
        "drone_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "M408 UAV",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      }
    ],
    "batteries": [
      {
        "name": "BATTERY-001",
        "battery_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "Multistar 6S 6600",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      },
      {
        "name": "BATTERY-002",
        "battery_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "Multistar 6S 8000",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      }
    ],
    "cameras": [
      {
        "name": "CAMERA-001",
        "camera_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "Huawei P30 Pro",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      },
      {
        "name": "CAMERA-002",
        "camera_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "Huawei P30 Pro X50",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      }
    ],
    "personnel": [
      {
        "name": "Jayson Beltran",
        "user_id": "0c5c21b6a42fadb018a5d1863c312345"
      },
      {
        "name": "Ahmed Major",
        "user_id": "0c5c21b6a42fadb018a5d1863c312345"
      }
    ],
    "lead": {
      "name": "Asher Solomon",
      "user_id": "0c5c21b6a42fadb018a5d1863c312345"
    },
    "purpose": [
      "Photography",
      "Analytics",
      "Security checks"
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

A deployment that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status.

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

```http
DELETE https://api.garuda.io/v2/flight/deployments/{deployment_id} HTTP/1.1
Host: api.garuda.io/v2
Accept: application/json

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
    "name": "Zhao Shi Chong's Deployment on 2018-05-22",
    "deployment_id": "0c5c21b6a42fadb018a5d1863c312345",
    "drones": [
      {
        "name": "DEV-001",
        "drone_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "M400 UAV",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      },
      {
        "name": "DEV-002",
        "drone_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "M408 UAV",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      }
    ],
    "batteries": [
      {
        "name": "BATTERY-001",
        "battery_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "Multistar 6S 6600",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      },
      {
        "name": "BATTERY-002",
        "battery_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "Multistar 6S 8000",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      }
    ],
    "cameras": [
      {
        "name": "CAMERA-001",
        "camera_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "Huawei P30 Pro",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      },
      {
        "name": "CAMERA-002",
        "camera_id": "0c5c21b6a42fadb018a5d1863c312345",
        "model_name": "Huawei P30 Pro X50",
        "model_id": "0c5c21b6a42fadb018a5d1863c312345"
      }
    ],
    "personnel": [
      {
        "name": "Jayson Beltran",
        "user_id": "0c5c21b6a42fadb018a5d1863c312345"
      },
      {
        "name": "Ahmed Major",
        "user_id": "0c5c21b6a42fadb018a5d1863c312345"
      }
    ],
    "lead": {
      "name": "Asher Solomon",
      "user_id": "0c5c21b6a42fadb018a5d1863c312345"
    },
    "purpose": [
      "Photography",
      "Analytics",
      "Security checks"
    ],
    "start_date": "1559571926000",
    "end_date": "1559572026000",
    "geo_json": "{ \"type\": \"Polygon\", \"coordinates\": [ [ [ -118.37099075317383, 33.85505651142062 ], [ -118.37305068969727, 33.85502978214579 ], [ -118.37347984313963, 33.854673391015496 ], [ -118.37306141853333, 33.85231226221667 ], [ -118.37193489074707, 33.85174201755203 ], [ -118.36997151374815, 33.85176874785573 ], [ -118.36995005607605, 33.8528112231754 ], [ -118.37099075317383, 33.85505651142062 ] ] ] }"
  }
}
```

`DELETE /flight/deployments/{deployment_id}`

Delete a specific deployment belonging to the company of the user. A valid `deployment_id` in the path parameter is required for a successful call.

<div></div>