## Flight Plans

Every flight requires a valid and approved `flight plan` before your drone can safely take off. There are many factors that need to be taken into account when creating a `flight plan`, including the `plan type`, `requirements`, `commands`, and more. Every `flight plan` must be tagged to an existing `deployment`, and each `flight plan` can be reused as required for multiple `flight sessions`. 

Each `flight plan` object will have the following properties:

| Property             | Type   | Description                                                                                            |
| -------------------- | ------ | ------------------------------------------------------------------------------------------------------ |
| `flight_plan_id`     | String | Unique flight plan ID                                                                                  |
| `deployment_id`      | String | Deployment ID that the flight plan is tagged to                                                        |
| `plan_type`          | String | The type of the flight plan                                                                            |
| `description`        | String | Description of the flight plan                                                                         |
| `last_modified_date` | String | Date of last modification to the flight plan in epoch (Unix timestamp), converted to milliseconds (ms) |
| `last_modified_by`   | String | User ID of the user that last modified the flight plan                                                 |
| `plan`               | Object | Object representing the details of the flight plan                                                     |

The `plan` object is represented by the following properties:

| Property       | Type   | Description                                                                                                                                                       |
| -------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `requirements` | Object | Object representing the requirements of the flight plan                                                                                                           |
| `commands`     | Array  | Array of objects representing the commands that will be executed during the flight plan. Each command is made up of an `id`, 7 `parameters`, and a `description`. |

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
  "description": "Take off (location TBD)"
}
```

The seven parameters are `Camera`, `Target`, `ReturnLocation`, `Navigate`, `Move`, `Yaw`, `TakeOff`, in that order. 

*(To flesh this part out with more details, including the requirements object, and also the plan_type - enum?)*

### Get all deployment flight plans

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans', params={

}, headers = headers)

print r.json()
```

```http
GET https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans HTTP/1.1
Host: api.garuda.io/v2
Accept: application/json

```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans',
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
      "flight_plan_id": "0c5c21b6a42fadb018a5d1863c312345",
      "deployment_id": "0c5c21b6a42fadb018a5d1863c312345",
      "plan_type": "ardupilot",
      "description": "Best flight plan ever",
      "last_modified_date": "string",
      "last_modified_by": "string",
      "plan": {
        "requirements": {},
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


`GET /flight/deployments/{deployment_id}/plans`

Get all flight plans of a specific deployment belonging to the company of the user. This will return a response containing an array of all the flight plan objects belonging to the specified deployment.

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

result = RestClient.post 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans',
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

r = requests.post('https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans', params={

}, headers = headers)

print r.json()

```

```http
POST https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans HTTP/1.1
Host: api.garuda.io/v2
Content-Type: application/json
Accept: application/json

```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "plan_type": "ardupilot",
  "description": "Best flight plan ever",
  "plan": {
    "requirements": {},
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

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans',
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
    "flight_plan_id": "0c5c21b6a42fadb018a5d1863c312345",
    "deployment_id": "0c5c21b6a42fadb018a5d1863c312345",
    "plan_type": "ardupilot",
    "description": "Best flight plan ever",
    "last_modified_date": "string",
    "last_modified_by": "string",
    "plan": {
      "requirements": {},
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

`POST /flight/deployments/{deployment_id}/plans`

Create a new flight plan for a deployment belonging to the company of the user. Note that the `deployment_id` parameter in the request URL has to be a valid `deployment_id` belonging to your company. 

You should pass in at minimum the following details in the request body:

| Property      | Type   | Description                                |
| ------------- | ------ | ------------------------------------------ |
| `plan_type`   | String | The type of the flight plan                |
| `description` | String | Description of the flight plan             |
| `plan`        | Object | Object representing the actual flight plan |

Refer to the description of the [flight plan object](#flight-plans) for details on each property.



<div></div>


### Get a flight plan

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans/{flight_plan_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans/{flight_plan_id}', params={

}, headers = headers)

print r.json()

```

```http
GET https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans/{flight_plan_id} HTTP/1.1
Host: api.garuda.io/v2
Accept: application/json

```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans/{flight_plan_id}',
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

`GET /flight/deployments/{deployment_id}/plans/{flight_plan_id}`

Get a specific flight plan for a deployment belonging to the company of the user.

> 200 Response

```json
{
  "success": true,
  "data": {
    "flight_plan_id": "0c5c21b6a42fadb018a5d1863c312345",
    "deployment_id": "0c5c21b6a42fadb018a5d1863c312345",
    "plan_type": "ardupilot",
    "description": "Best flight plan ever",
    "last_modified_date": "string",
    "last_modified_by": "string",
    "plan": {
      "requirements": {},
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

result = RestClient.patch 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans/{flight_plan_id}',
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

r = requests.patch('https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans/{flight_plan_id}', params={

}, headers = headers)

print r.json()

```

```http
PATCH https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans/{flight_plan_id} HTTP/1.1
Host: api.garuda.io/v2
Content-Type: application/json
Accept: application/json

```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "plan_type": "ardupilot",
  "description": "Best flight plan ever",
  "plan": {
    "requirements": {},
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

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans/{flight_plan_id}',
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
    "flight_plan_id": "0c5c21b6a42fadb018a5d1863c312345",
    "deployment_id": "0c5c21b6a42fadb018a5d1863c312345",
    "plan_type": "ardupilot",
    "description": "Best flight plan ever",
    "last_modified_date": "string",
    "last_modified_by": "string",
    "plan": {
      "requirements": {},
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


`PATCH /flight/deployments/{deployment_id}/plans/{flight_plan_id}`

Update a specific flight plan for a deployment belonging to the company of the user.

To update a flight plan, you can pass in any subset of the properties of the flight plan in the request body. All properties are optional.

| Property             | Type   | Description                                                                                            |
| -------------------- | ------ | ------------------------------------------------------------------------------------------------------ |
| `flight_plan_id`     | String | Unique flight plan ID                                                                                  |
| `deployment_id`      | String | Deployment ID that the flight plan is tagged to                                                        |
| `plan_type`          | String | The type of the flight plan                                                                            |
| `description`        | String | Description of the flight plan                                                                         |
| `last_modified_date` | String | Date of last modification to the flight plan in epoch (Unix timestamp), converted to milliseconds (ms) |
| `last_modified_by`   | String | User ID of the user that last modified the flight plan                                                 |
| `plan`               | Object | Object representing the details of the flight plan                                                     |

A flight plan that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status.

<div></div>

### Delete a flight plan

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans/{flight_plan_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans/{flight_plan_id}', params={

}, headers = headers)

print r.json()

```

```http
DELETE https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans/{flight_plan_id} HTTP/1.1
Host: api.garuda.io/v2
Accept: application/json

```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}/plans/{flight_plan_id}',
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

`DELETE /flight/deployments/{deployment_id}/plans/{flight_plan_id}`

Delete a specific flight plan for a deployment belonging to the company of the user.

> 200 Response

```json
{
  "success": true,
  "data": {
    "flight_plan_id": "0c5c21b6a42fadb018a5d1863c312345",
    "deployment_id": "0c5c21b6a42fadb018a5d1863c312345",
    "plan_type": "ardupilot",
    "description": "Best flight plan ever",
    "last_modified_date": "string",
    "last_modified_by": "string",
    "plan": {
      "requirements": {},
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
