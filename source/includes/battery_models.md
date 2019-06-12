## Battery Models

Fleet APIs allow you to manage battery models. Each `battery_model` object contains information regarding a specific battery model provided by a battery provider. A `battery_model` object has the following properties:

| Property         | Type   | Description                                                                                         |
| ---------------- | ------ | --------------------------------------------------------------------------------------------------- |
| `name`           | String | Name of the battery model                                                                           |
| `model_id`       | String | Battery model ID                                                                                    |
| `provider`       | Object | Object representing the battery provider. Contains the `name` of the provider and the `provider_id` |
| `chemistry`      | String | The chemistry composition of the battery                                                            |
| `series`         | String | Enumerated string description of the series settings of the battery                                 |
| `parallel`       | String | Enumerated string description of the parallel settings of the battery                               |
| `capacity`       | String | Capacity of the battery in milliamp-hours (mAh)                                                     |
| `weight`         | String | Weight of the battery in kilograms (kg)                                                             |
| `discharge_rate` | String | String description of the discharge rate of the battery                                             |
| `dimensions`     | Object | Dimensions of drone. Object has the properties `width`, `length`, and `height` (m)                  |

The `series` and `parallel` characteristic of the battery will only accept pre-defined enumerations. They are listed as follows:

| Series                                                                    |
| ------------------------------------------------------------------------- |
| `1S`, `2S`, `3S`, `4S`, `5S`, `6S`, `7S`, `8S`, `9S`, `10S`, `11S`, `12S` |

| Parallel               |
| ---------------------- |
| `1P`, `2P`, `3P`, `4P` |

### Get all battery models

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models',
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
      "name": "Multistar 6S 6600",
      "model_id": "4b38b7383fdb23fbff8c3a6a694e4533",
      "provider": {
        "name": "DJI",
        "provider_id": "1c9e81a9a3352cd010857331acd63a92"
      },
      "chemistry": "LiPo",
      "series": "6",
      "parallel": "1",
      "capacity": "6600"
    }
  ]
}
```

`GET /fleet/battery-providers/{battery_provider_id}/battery-models`

When getting all `battery_models` belonging to a specific battery provider in your company, you have to provide a valid and existing `battery_provider_id`. The HTTP response body will contain an array of `battery_model` objects belonging to your specified `battery_provider`.

You can specify the extent of which to fetch the data via query strings:

| Query     | Default   | Values            | Description                                                 |
| --------- | --------- | ----------------- | ----------------------------------------------------------- |
| `options` | `shallow` | `shallow`, `deep` | Specify if data retrieved should be a deep or shallow fetch |

For a `shallow` fetch (which is the default behaviour), only the `name`, `model_id`, `provider`, `chemistry`, `series`, `parallel`, and `capacity` will be retrieved (see sample response on the left for how this will look like). A `deep` fetch will retrieve more information for each of the objects -- to see the exact properties that will be retrieved with a `deep` fetch, refer to the [beginning of this section](#battery-models).

<div></div>

### Create new battery model

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models',
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

r = requests.post('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models', params={

}, headers = headers)

print r.json()

```

```shell
curl -X POST 'https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "name": "Multistar 6S 6600",
      "provider_id": "1c9e81a9a3352cd010857331acd63a92",
      "chemistry": "LiPo",
      "series": "6",
      "parallel": "1",
      "capacity": "6600"
     }'
```


```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "name": "Multistar 6S 6600",
  "provider_id": "1c9e81a9a3352cd010857331acd63a92",
  "chemistry": "LiPo",
  "series": "6",
  "parallel": "1",
  "capacity": "6600"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models',
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
    "name": "Multistar 6S 6600",
    "model_id": "4b38b7383fdb23fbff8c3a6a694e4533",
    "provider": {
      "name": "DJI",
      "provider_id": "1c9e81a9a3352cd010857331acd63a92"
    },
    "chemistry": "LiPo",
    "series": "6",
    "parallel": "1",
    "capacity": "6600"
  }
}
```


`POST /fleet/battery-providers/{battery_provider_id}/battery-models`

Every created `battery_model` has to belong to a valid and existing `battery_provider`. When calling this API, the `battery_provider_id` parameter has to be valid for a successful call.

When creating a new `battery_model`, at minimum, you should pass in values for the following properties:

| Property      | Type   | Description                                                           |
| ------------- | ------ | --------------------------------------------------------------------- |
| `name`        | String | Name of the battery model                                             |
| `provider_id` | String | Battery provider ID                                                   |
| `chemistry`   | String | The chemistry composition of the battery                              |
| `series`      | String | Enumerated string description of the series settings of the battery   |
| `parallel`    | String | Enumerated string description of the parallel settings of the battery |
| `capacity`    | String | Capacity of the battery in milliamp-hours (mAh)                       |

For more information on these properties, refer to the `battery_model` object description at the [beginning of this section](#battery-models)

You can also choose to pass in more information on the battery model to flesh out the rest of the object:

| Property         | Type   | Description                                                                        |
| ---------------- | ------ | ---------------------------------------------------------------------------------- |
| `weight`         | String | Weight of the battery in kilograms (kg)                                            |
| `discharge_rate` | String | String description of the discharge rate of the battery                            |
| `dimensions`     | Object | Dimensions of drone. Object has the properties `width`, `length`, and `height` (m) |

Otherwise, these properties can also be added at a later time with the [`PATCH` endpoint](#update-a-battery-model).

<div></div>

### Update a battery model

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.patch 'https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models/{battery_model_id}',
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

r = requests.patch('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models/{battery_model_id}', params={

}, headers = headers)

print r.json()

```


```shell
curl -X PATCH 'https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models/{battery_model_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "dimensions": {
        "width": "0.056",
        "length": "0.0145",
        "height": "0.052"
      }
     }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "dimensions": {
    "width": "0.056",
    "length": "0.0145",
    "height": "0.052"
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models/{battery_model_id}',
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
    "name": "Multistar 6S 6600",
    "model_id": "4b38b7383fdb23fbff8c3a6a694e4533",
    "provider": {
      "name": "DJI",
      "provider_id": "1c9e81a9a3352cd010857331acd63a92"
    },
    "chemistry": "LiPo",
    "series": "6",
    "parallel": "1",
    "capacity": "6600",
    "dimensions": {
      "width": "0.056",
      "length": "0.0145",
      "height": "0.052"
    }
  }
}
```

`PATCH /fleet/battery-providers/{battery_provider_id}/battery-models/{battery_model_id}`

This endpoint allows you to edit and update information regarding a `battery_model` that has already been created. For the request body of this endpoint, it is not necessary to pass in values for all the properties of a `battery_model`. All of the following properties are optional: 

| Property         | Type   | Description                                                                                         |
| ---------------- | ------ | --------------------------------------------------------------------------------------------------- |
| `name`           | String | Name of the battery model                                                                           |
| `model_id`       | String | Battery model ID                                                                                    |
| `provider`       | Object | Object representing the battery provider. Contains the `name` of the provider and the `provider_id` |
| `chemistry`      | String | The chemistry composition of the battery                                                            |
| `series`         | String | Enumerated string description of the series settings of the battery                                 |
| `parallel`       | String | Enumerated string description of the parallel settings of the battery                               |
| `capacity`       | String | Capacity of the battery in milliamp-hours (mAh)                                                     |
| `weight`         | String | Weight of the battery in kilograms (kg)                                                             |
| `discharge_rate` | String | String description of the discharge rate of the battery                                             |
| `dimensions`     | Object | Dimensions of drone. Object has the properties `width`, `length`, and `height` (m)                  |

For more information on these properties, refer to the `battery_model` object description at the [beginning of this section](#battery-models)

A `battery_model` that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status. Response body will also contain the updated `battery_model` object.

<div></div>

### Delete a battery model

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models/{battery_model_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models/{battery_model_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X DELETE 'https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models/{battery_model_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/battery-providers/{battery_provider_id}/battery-models/{battery_model_id}',
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
    "name": "Multistar 6S 6600",
    "model_id": "4b38b7383fdb23fbff8c3a6a694e4533",
    "provider": {
      "name": "DJI",
      "provider_id": "1c9e81a9a3352cd010857331acd63a92"
    },
    "chemistry": "LiPo",
    "series": "6",
    "parallel": "1",
    "capacity": "6600"
  }
}
```

`DELETE /fleet/battery-providers/{battery_provider_id}/battery-models/{battery_model_id}`

Delete a specific battery model of a specific battery provider belonging to the company of the user.
