## Flight Sessions

Once you have your flight plan approved, you are ready to fly! 

Each drone flight is represented by a flight session. Each `flight session` must be tagged to a valid and approved `flight plan` and an existing `deployment`. This set of endpoints allow you to manage and log the flight history of your deployments easily.

A `flight session` essentially tracks the `flight plan` of the flight, as well as the start and end time of the flight. A `flight session` has the following properties:

| Property          | Type   | Description                                                                          |
| ----------------- | ------ | ------------------------------------------------------------------------------------ |
| `deployment_id`   | String | A valid deployment ID                                                                |
| `flight_plan_id`  | String | A valid and approved flight plan ID                                                  |
| `start_date_time` | String | Start time of flight session in epoch (Unix timestamp), converted to milliseconds    |
| `end_date_time`   | String | End time of flight session in epoch (Unix timestamp), converted to milliseconds (ms) |

### Get all deployment flight sessions

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions',
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
      "flight_session_id": "0b28db84d57ea15b5c26e5c3ffce67fc",
      "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
      "deployment_id": "9703889c2bb4322025815ed1a0509eba",
      "start_date_time": 1527469200000,
      "end_date_time": 1527479200000
    }
  ]
}
```

`GET /flight/deployments/{deployment_id}/sessions`

Get all flight sessions of a specific deployment belonging to the company of the user.

<div></div>

### Create new flight session

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions',
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

r = requests.post('https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions', params={

}, headers = headers)

print r.json()

```

```shell
curl -X POST 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
      "start_date_time": 1527469200000,
      "end_date_time": 1527479200000
     }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
  "start_date_time": 1527469200000,
  "end_date_time": 1527479200000
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions',
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
    "flight_session_id": "0b28db84d57ea15b5c26e5c3ffce67fc",
    "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
    "deployment_id": "9703889c2bb4322025815ed1a0509eba",
    "start_date_time": 1527469200000,
    "end_date_time": 1527479200000
  }
}
```
`POST /flight/deployments/{deployment_id}/sessions`

This endpoint allows you to create a new `flight session` for a specific deployment. Note that the `deployment_id` parameter in the request URL has to be a valid `deployment_id` belonging to your company. 

You should pass in at minimum the following details in the request body:

| Item              | Type   | Description                                                                          |
| ----------------- | ------ | ------------------------------------------------------------------------------------ |
| `flight_plan_id`  | String | A valid and approved flight plan ID                                                  |
| `start_date_time` | String | Start time of flight session in epoch (Unix timestamp), converted to milliseconds    |
| `end_date_time`   | String | End time of flight session in epoch (Unix timestamp), converted to milliseconds (ms) |

<div></div>

### Get a flight session

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions/{flight_session_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions/{flight_session_id}', params={

}, headers = headers)

print r.json()

```


```shell
curl -X GET 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions/{flight_session_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions/{flight_session_id}',
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
    "flight_session_id": "0b28db84d57ea15b5c26e5c3ffce67fc",
    "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
    "deployment_id": "9703889c2bb4322025815ed1a0509eba",
    "start_date_time": 1527469200000,
    "end_date_time": 1527479200000
  }
}
```
`GET /flight/deployments/{deployment_id}/sessions/{flight_session_id}`

Get a specific flight session for a deployment belonging to the company of the user.

### Update a flight session

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.patch 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions/{flight_session_id}',
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

r = requests.patch('https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions/{flight_session_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X PATCH 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions/{flight_session_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
       "end_date_time": 1527480200000
     }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "end_date_time": 1527480200000
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions/{flight_session_id}',
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
    "flight_session_id": "0b28db84d57ea15b5c26e5c3ffce67fc",
    "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
    "deployment_id": "9703889c2bb4322025815ed1a0509eba",
    "start_date_time": 1527469200000,
    "end_date_time": 1527480200000
  }
}
```

`PATCH /flight/deployments/{deployment_id}/sessions/{flight_session_id}`

Update a specific flight session for a deployment belonging to the company of the user.

To update a flight session, you can pass in any subset of the properties of the flight session in the request body. All properties are optional.

| Property          | Type   | Description                                                                          |
| ----------------- | ------ | ------------------------------------------------------------------------------------ |
| `start_date_time` | String | Start time of flight session in epoch (Unix timestamp), converted to milliseconds    |
| `end_date_time`   | String | End time of flight session in epoch (Unix timestamp), converted to milliseconds (ms) |

A flight session that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status.

<div></div>

### Delete a flight session

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions/{flight_session_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions/{flight_session_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X DELETE 'https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions/{flight_session_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/flight/deployments/{deployment_id}/sessions/{flight_session_id}',
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
    "flight_session_id": "0b28db84d57ea15b5c26e5c3ffce67fc",
    "flight_plan_id": "fc5583b754db73cc526a6ffa919d393a",
    "deployment_id": "9703889c2bb4322025815ed1a0509eba",
    "start_date_time": 1527469200000,
    "end_date_time": 1527479200000
  }
}
```

`DELETE /flight/deployments/{deployment_id}/sessions/{flight_session_id}`

Delete a specific flight session for a deployment belonging to the company of the user.

A successful deletion will return a `200 OK` status and the deleted flight session object in the response body.

<div></div>

