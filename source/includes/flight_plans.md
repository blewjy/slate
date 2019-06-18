## Flight Plans

Every flight requires a valid and approved `flight plan` before your drone can safely take off. There are many factors that need to be taken into account when creating a `flight plan`, including the `plan type`, `requirements`, `commands`, and more. Every `flight plan` must be tagged to an existing `deployment`, and each `flight plan` can be reused as required for multiple `flight sessions`. 

> A full `flight_plan` object, including all optional properties

```json
{
  "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
  "deployment_id": "9703889c2bb4322025815ed1a0509eba",
  "company_id": "ca42ab884a633d6a823b45e6ebe9534c",
  "description": "FLIGHTPLAN-001",
  "last_modified_date": "1245591926000",
  "last_modified_by": "3b20c067ab91da9436ddaea6b83a9536",
  "plan_type": "ardupilot",
  "plan": {
    "requirements": {
      "RTL_ALT": 3000,
      "FS_BATT_ENABLE": 2,
      "FS_GCS_ENABLE": 2,
      "FS_THR_ENABLE": 1
    },
    "commands": [
      {
        "id": "22",
        "param1": "",
        "param2": "",
        "param3": "",
        "param4": "",
        "param5": "",
        "param6": "",
        "param7": "30",
        "description": "Take off (location TBD)"
      }
    ],
    "home_location": {
      "lat": "1.0",
      "lng": "103.0"
    },
    "rtl_path": [
      {
        "id": "20",
        "param1": "",
        "param2": "",
        "param3": "",
        "param4": "",
        "param5": "",
        "param6": "",
        "param7": "",
        "description": "Survey complete, return to launch location"
      }
    ]
  }
}
```

Each `flight plan` object will have the following properties:

| Property             | Type   | Description                                                                                        |
| -------------------- | ------ | -------------------------------------------------------------------------------------------------- |
| `flight_plan_id`     | String | Unique flight plan ID                                                                              |
| `deployment_id`      | String | Deployment ID that the flight plan is tagged to                                                    |
| `company_id`         | String | Unique company ID                                                                                  |
| `description`        | String | Description of the flight plan                                                                     |
| `last_modified_date` | String | Date of last modification to flight plan in epoch (Unix timestamp), converted to milliseconds (ms) |
| `last_modified_by`   | String | User ID of the user that last modified the flight plan                                             |
| `plan_type`          | String | The type of the flight plan: currently only `arudpilot` is supported                               |
| `plan`               | Object | Object representing the details of the flight plan                                                 |

The `plan` object is represented by the following properties:

| Property        | Type   | Description                                                                                                                                                                                                                                                                                                                                |
| --------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `requirements`  | Object | Object representing the requirements of the flight plan. Requirements to be described as parameters. 4 different parameters are supported: `RTL_ALT`, `FS_BATT_ENABLE`, `FS_GCS_ENABLE`, `FS_THR_ENABLE`. Refer to the [ardupilot documentation](http://ardupilot.org/copter/docs/introduction.html#) for information on these parameters. |
| `commands`      | Array  | Array of objects representing the commands that will be executed during the flight plan. Each command is made up of an `id`, 7 `parameters`, a `description` and some optional `properties`.                                                                                                                                               |
| `home_location` | Object | Object with properties `lat` and `lng`, specifying where the drone will take off from. This property is optional.                                                                                                                                                                                                                          |
| `rtl_path`      | Array  | Array of objects representing the commands that define a custom 'Return To Launch' (RTL) path that will override the default RTL behaviour. This property is optional.                                                                                                                                                                     |

A `command` object has the following JSON format:

<div class="center-column"></div>

```json
{
  "id": "22",
  "param1": "15",
  "param2": "16",
  "param3": "17",
  "param4": "18",
  "param5": "19",
  "param6": "20",
  "param7": "21",
  "description": "Take off (location TBD)",
  "properties": { // Optional properties
    "conditionYawTarget": { 
        "lat": "2.0",
        "lng": "104.0"
    }
  }
}
```

The seven parameters are `Camera`, `Target`, `ReturnLocation`, `Navigate`, `Move`, `Yaw`, `TakeOff`, in that order. 

### Get all flight plans

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/flight/plans',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/flight/plans', params={

}, headers = headers)

print r.json()
```

```shell
curl -X GET 'https://api.garuda.io/v2/flight/plans' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/plans',
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
      "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
      "deployment_id": "9703889c2bb4322025815ed1a0509eba",
      "company_id": "ca42ab884a633d6a823b45e6ebe9534c",
      "description": "FLIGHTPLAN-001",
      "last_modified_date": "1245591926000",
      "last_modified_by": "3b20c067ab91da9436ddaea6b83a9536",
      "plan_type": "ardupilot",
      "plan": {
        "requirements": {
          "RTL_ALT": 3000,
     			"FS_BATT_ENABLE": 2,
     			"FS_GCS_ENABLE": 2,
     			"FS_THR_ENABLE": 1
        },
        "commands": [
          {
            "id": "22",
            "param1": "15",
            "param2": "16",
            "param3": "17",
            "param4": "18",
            "param5": "19",
            "param6": "20",
            "param7": "21",
            "description": "Take off (location TBD)"
          }
        ]
      }
    }
  ]
}
```

`GET /flight/plans`

`GET /flight/plans?deployment_id=`

You can get all flight plans belonging to your company or belonging to a specific deplyoment via this endpoint. If you wish to filter and retrieve flight plans from only a specific deployment, you should specify the `deployment_id` via the query string. Otherwise, if no `deployment_id` is specified, all flight plans belonging to your company will be retrieved.

The response body of this endpoint will contain an array of all the `flight_plan` objects.

<div></div>

### Create new flight plan

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.garuda.io/v2/flight/plans',
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

r = requests.post('https://api.garuda.io/v2/flight/plans', params={

}, headers = headers)

print r.json()

```

```shell
curl -X POST 'https://api.garuda.io/v2/flight/plans' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "description": "FLIGHTPLAN-001",
      "plan_type": "ardupilot",
      "plan": {
        "requirements": {
          "RTL_ALT": 3000,
          "FS_BATT_ENABLE": 2,
          "FS_GCS_ENABLE": 2,
          "FS_THR_ENABLE": 1
        },
        "commands": [
          {
            "id": "22",
            "param1": "15",
            "param2": "16",
            "param3": "17",
            "param4": "18",
            "param5": "19",
            "param6": "20",
            "param7": "21",
            "description": "Take off (location TBD)"
          }
        ]
      }
    }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "description": "FLIGHTPLAN-001",
  "plan_type": "ardupilot",
  "plan": {
    "requirements": {
      "RTL_ALT": 3000,
      "FS_BATT_ENABLE": 2,
      "FS_GCS_ENABLE": 2,
      "FS_THR_ENABLE": 1
    },
    "commands": [
      {
        "id": "22",
        "param1": "15",
        "param2": "16",
        "param3": "17",
        "param4": "18",
        "param5": "19",
        "param6": "20",
        "param7": "21",
        "description": "Take off (location TBD)"
      }
    ]
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/plans',
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
    "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
    "deployment_id": "9703889c2bb4322025815ed1a0509eba",
    "company_id": "ca42ab884a633d6a823b45e6ebe9534c",
    "description": "FLIGHTPLAN-001",
    "last_modified_date": "1245591926000",
    "last_modified_by": "3b20c067ab91da9436ddaea6b83a9536",
    "plan_type": "ardupilot",
    "plan": {
      "requirements": {
        "RTL_ALT": 3000,
        "FS_BATT_ENABLE": 2,
        "FS_GCS_ENABLE": 2,
        "FS_THR_ENABLE": 1
      },
      "commands": [
        {
          "id": "22",
          "param1": "15",
          "param2": "16",
          "param3": "17",
          "param4": "18",
          "param5": "19",
          "param6": "20",
          "param7": "21",
          "description": "Take off (location TBD)"
        }
      ]
    }
  }
}
```

`POST /flight/plans`

Create a new flight plan for a deployment belonging to the company of the user.

You should pass in at minimum the following details in the request body:

| Property        | Type   | Description                                    |
| --------------- | ------ | ---------------------------------------------- |
| `deployment_id` | String | Valid deployment ID tagged to this flight plan |
| `plan_type`     | String | The type of the flight plan                    |
| `description`   | String | Description of the flight plan                 |
| `plan`          | Object | Object representing the actual flight plan     |

Within the `plan` object, there are some properties that are optional:

| Property        | Type   | Required  | Description                                                                                                                 |
| --------------- | ------ | --------- | --------------------------------------------------------------------------------------------------------------------------- |
| `requirements`  | Object | **true**  | Requirements of the flight plan. Object containing properties `RTL_ALT`, `FS_BATT_ENABLE`, `FS_GCS_ENABLE`, `FS_THR_ENABLE` |
| `commands`      | Array  | **true**  | Array of command objects representing the flight plan.                                                                      |
| `home_location` | Object | **false** | Object with properties `lat` and `long`, specifying the home location of the flight.                                        |
| `rtl_path`      | Array  | **false** | Array of command objects representing a custom RTL path.                                                                    |

Refer to the description of the [flight plan object](#flight-plans) for more details on each property.

<div></div>


### Get a flight plan

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/flight/plans/{flight_plan_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/flight/plans/{flight_plan_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/flight/plans/{flight_plan_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/plans/{flight_plan_id}',
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

`GET /flight/plans/{flight_plan_id}`

Get a specific flight plan for a deployment belonging to the company of the user.

> 200 Response

```json
{
  "success": true,
  "data": {
    "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
    "deployment_id": "9703889c2bb4322025815ed1a0509eba",
    "company_id": "ca42ab884a633d6a823b45e6ebe9534c",
    "description": "FLIGHTPLAN-001",
    "last_modified_date": "1245591926000",
    "last_modified_by": "3b20c067ab91da9436ddaea6b83a9536",
    "plan_type": "ardupilot",
    "plan": {
      "requirements": {
        "RTL_ALT": 3000,
        "FS_BATT_ENABLE": 2,
        "FS_GCS_ENABLE": 2,
        "FS_THR_ENABLE": 1
      },
      "commands": [
        {
          "id": "22",
          "param1": "15",
          "param2": "16",
          "param3": "17",
          "param4": "18",
          "param5": "19",
          "param6": "20",
          "param7": "21",
          "description": "Take off (location TBD)"
        }
      ]
    }
  }
}
```

### Update a flight plan

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.patch 'https://api.garuda.io/v2/flight/plans/{flight_plan_id}',
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

r = requests.patch('https://api.garuda.io/v2/flight/plans/{flight_plan_id}', params={

}, headers = headers)

print r.json()

```

```http
PATCH https://api.garuda.io/v2/flight/plans/{flight_plan_id} HTTP/1.1
Host: api.garuda.io/v2
Content-Type: application/json
Accept: application/json

```

```shell
curl -X PATCH 'https://api.garuda.io/v2/flight/plans/{flight_plan_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "description": "FLIGHTPLAN-001_rev-1"
    }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "description": "FLIGHTPLAN-001_rev-1"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/plans/{flight_plan_id}',
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
    "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
    "deployment_id": "9703889c2bb4322025815ed1a0509eba",
    "company_id": "ca42ab884a633d6a823b45e6ebe9534c",
    "description": "FLIGHTPLAN-001_rev-1",
    "last_modified_date": "1245591926000",
    "last_modified_by": "3b20c067ab91da9436ddaea6b83a9536",
    "plan_type": "ardupilot",
    "plan": {
      "requirements": {
        "RTL_ALT": 3000,
        "FS_BATT_ENABLE": 2,
        "FS_GCS_ENABLE": 2,
        "FS_THR_ENABLE": 1
      },
      "commands": [
        {
          "id": "22",
          "param1": "15",
          "param2": "16",
          "param3": "17",
          "param4": "18",
          "param5": "19",
          "param6": "20",
          "param7": "21",
          "description": "Take off (location TBD)"
        }
      ]
    }
  }
}
```

`PATCH /flight/plans/{flight_plan_id}`

To update a flight plan, you can pass in any subset of the following properties in the request body:

| Property        | Type   | Description                                                                                    |
| --------------- | ------ | ---------------------------------------------------------------------------------------------- |
| `deployment_id` | String | A valid deployment ID that the flight plan is tagged to                                        |
| `plan_type`     | String | The type of the flight plan                                                                    |
| `description`   | String | Description of the flight plan                                                                 |
| `requirements`  | Object | Requirements of the flight plan.                                                               |
| `commands`      | Array  | Array of objects representing the commands that will be executed during the flight plan.       |
| `home_location` | Object | Object with properties `lat` and `lng`, specifying where the drone will take off from.         |
| `rtl_path`      | Array  | Array of objects representing the commands that define a custom 'Return To Launch' (RTL) path. |

Only the properties specified in the request body will be updated in the `flight_plan`, and the rest of the properties will remain unchanged. For more detailed information on these properties, refer to the specification at the [start of this section](#flight-plans).

A flight plan that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status. The response body will also contain the updated `flight_plan` object.

<div></div>

### Delete a flight plan

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/flight/plans/{flight_plan_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/flight/plans/{flight_plan_id}', params={

}, headers = headers)

print r.json()

```


```shell
curl -X DELETE 'https://api.garuda.io/v2/flight/plans/{flight_plan_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/plans/{flight_plan_id}',
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

`DELETE /flight/plans/{flight_plan_id}`

Delete a specific flight plan for a deployment belonging to the company of the user.

A successful deletion will return a `200 OK` status and the deleted flight plan object in the response body.

> 200 Response

```json
{
  "success": true,
  "data": {
    "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
    "deployment_id": "9703889c2bb4322025815ed1a0509eba",
    "company_id": "ca42ab884a633d6a823b45e6ebe9534c",
    "description": "FLIGHTPLAN-001",
    "last_modified_date": "1245591926000",
    "last_modified_by": "3b20c067ab91da9436ddaea6b83a9536",
    "plan_type": "ardupilot",
    "plan": {
      "requirements": {
        "RTL_ALT": 3000,
        "FS_BATT_ENABLE": 2,
        "FS_GCS_ENABLE": 2,
        "FS_THR_ENABLE": 1
      },
      "commands": [
        {
          "id": "22",
          "param1": "15",
          "param2": "16",
          "param3": "17",
          "param4": "18",
          "param5": "19",
          "param6": "20",
          "param7": "21",
          "description": "Take off (location TBD)"
        }
      ]
    }
  }
}
```
