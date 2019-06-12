
## Camera Models

Fleet APIs allow you to manage camera models. Each `camera_model` object contains information regarding a specific camera model provided by a camera provider. A `camera_model` object has the following properties:

| Property     | Type   | Description                                                                                        |
| ------------ | ------ | -------------------------------------------------------------------------------------------------- |
| `name`       | String | Name of the camera model                                                                           |
| `model_id`   | String | Camera model ID                                                                                    |
| `provider`   | Object | Object representing the camera provider. Contains the `name` of the provider and the `provider_id` |
| `weight`     | String | Weight of the camera in kilograms (kg)                                                             |
| `type`       | Array  | Array of enumerated strings describing the type of the camera. (see below)                         |
| `properties` | Object | Object representing the properties of this camera model. (see below)                               |

Each `camera_model` should be of one or both of 2 types, and this is specified under the `type` property of the `camera_model` object. The enumerations available for `type` are:

| Type          |
| ------------- |
| `RGB`, `NDVI` |

Each `camera_model` has a set of `properties` that describes the specifications of the camera model. The `properties` in the `camera_model` is an object with the following properties:

| Property                       | Type    | Description                                                                          |
| ------------------------------ | ------- | ------------------------------------------------------------------------------------ |
| `sensor_size`                  | String  | sensor_size                                                                          |
| `image_modes`                  | Array   | Array of strings of image_modes                                                      |
| `video_modes`                  | Array   | Array of strings of video_modes                                                      |
| `maximum_clip_length`          | String  | maximum_clip_length                                                                  |
| `image_file_formats`           | Array   | Array of strings of supported image file formats                                     |
| `video_file_formats`           | Array   | Array of strings of supported video file formats                                     |
| `lens_focal_length`            | String  | lens_focal_length                                                                    |
| `lens_focal_length_35mm_equiv` | String  | lens_focal_length_35mm_equiv                                                         |
| `optical_zoom`                 | String  | optical_zoom                                                                         |
| `digital_zoom`                 | String  | digital_zoom                                                                         |
| `aperture`                     | String  | aperture                                                                             |
| `image_stabilization`          | String  | image_stabilization                                                                  |
| `auto_focus`                   | String  | auto_focus                                                                           |
| `manual_focus`                 | Boolean | Whether manual focus mode is supported                                               |
| `af_modes`                     | Array   | Array of strings of supported AF Modes                                               |
| `af_lock`                      | Boolean | Whether AF lock is on                                                                |
| `af_assist_lamp`               | Boolean | Whether AF assist lamp is on                                                         |
| `focus_distance`               | String  | focus_distance                                                                       |
| `metering`                     | Array   | Array of strings describing the metering                                             |
| `max_iso`                      | String  | max_iso                                                                              |
| `shutter_speed`                | String  | shutter_speed                                                                        |
| `modes`                        | Array   | Array of strings describing the camera modes                                         |
| `white_balance`                | Array   | Array of strings of white balance modes(?)                                           |
| `continuous_shooting`          | String  | continuous_shooting                                                                  |
| `connectivity`                 | Array   | Array of strings of supported connections                                            |
| `storage`                      | Array   | Array of strings of supported storage                                                |
| `power`                        | String  | power                                                                                |
| `dimensions`                   | Object  | Object representing dimensions of camera. Properties are `width`, `length`, `height` |

### Get all camera models

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models', params={

}, headers = headers)

print r.json()

```

```shell
curl -X GET 'https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models',
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
      "name": "Powershot S100",
      "model_id": "0e51493cd1ae85c097547de808642659",
      "provider": {
        "name": "Canon Inc.",
        "provider_id": "2db274b2709ce1ce89457057d6e9fd3b"
      },
      "type": [
        "RGB", 
        "NDIV"
      ]
    }
  ]
}
```

`GET /fleet/camera-providers/{camera_provider_id}/camera-models`

When getting all `camera_models` belonging to a specific camera provider in your company, you have to provide a valid and existing `camera_provider_id`. The HTTP response body will contain an array of `camera_model` objects belonging to your specified `camera_provider`.

You can specify the extent of which to fetch the data via query strings:

| Query     | Default   | Values            | Description                                                 |
| --------- | --------- | ----------------- | ----------------------------------------------------------- |
| `options` | `shallow` | `shallow`, `deep` | Specify if data retrieved should be a deep or shallow fetch |

For a `shallow` fetch (which is the default behaviour), only the `name`, `model_id`, `provider`, and `type` will be retrieved (see sample response on the left for how this will look like). A `deep` fetch will retrieve more information for each of the objects -- to see the exact properties that will be retrieved with a `deep` fetch, refer to the [beginning of this section](#camera-models).

<div></div>

### Create new camera model

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models',
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

r = requests.post('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models', params={

}, headers = headers)

print r.json()

```

```shell
curl -X POST 'https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "name": "Powershot S100",
      "provider_id": "2db274b2709ce1ce89457057d6e9fd3b"
      "type": [
        "RGB", 
        "NDIV"
      ]
     }'
```


```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "name": "Powershot S100",
  "provider_id": "2db274b2709ce1ce89457057d6e9fd3b"
  "type": [
    "RGB", 
    "NDIV"
  ]
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models',
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
    "name": "Powershot S100",
    "model_id": "0e51493cd1ae85c097547de808642659",
    "provider": {
      "name": "Canon Inc.",
      "provider_id": "2db274b2709ce1ce89457057d6e9fd3b"
    },
    "type": [
      "RGB", 
      "NDIV"
    ]
  }
}
```


`POST /fleet/camera-providers/{camera_provider_id}/camera-models`

Every created `camera_model` has to belong to a valid and existing `camera_provider`. When calling this API, the `camera_provider_id` parameter has to be valid for a successful call.

When creating a new `camera_model`, at minimum, you should pass in values for the following properties:

| Property      | Type   | Description                                                                      |
| ------------- | ------ | -------------------------------------------------------------------------------- |
| `name`        | String | Name of the camera model                                                         |
| `provider_id` | String | Camera provider ID                                                               |
| `type`        | Array  | Array of [enumerated strings](#camera-models) describing the type of the camera. |

For more information on these properties, refer to the `camera_model` object description at the [beginning of this section](#camera-models)

You can also choose to pass in more information on the camera model to flesh out the rest of the object:

| Property     | Type   | Description                                                          |
| ------------ | ------ | -------------------------------------------------------------------- |
| `weight`     | String | Weight of the camera in kilograms (kg)                               |
| `properties` | Object | Object representing the properties of this camera model. (see below) |

Otherwise, these properties can also be added at a later time with the [`PATCH` endpoint](#update-a-camera-model).

<div></div>

### Update a camera model

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.patch 'https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models/{camera_model_id}',
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

r = requests.patch('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models/{camera_model_id}', params={

}, headers = headers)

print r.json()

```


```shell
curl -X PATCH 'https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models/{camera_model_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
     -d '{
      "weight": "0.198",
      "properties": {
        "video_modes": [
          "1920 x 1080 @ 24 fps",
          "1280 x 720 @ 30fps"
        ],
        "video_file_formats": [
          "H.264"
        ]
      }
     }'
```

```javascript
const fetch = require('node-fetch');
const inputBody = '{
  "weight": "0.198",
  "properties": {
    "video_modes": [
      "1920 x 1080 @ 24 fps",
      "1280 x 720 @ 30fps"
    ],
    "video_file_formats": [
      "H.264"
    ]
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models/{camera_model_id}',
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
    "name": "Powershot S100",
    "model_id": "0e51493cd1ae85c097547de808642659",
    "provider": {
      "name": "Canon Inc.",
      "provider_id": "2db274b2709ce1ce89457057d6e9fd3b"
    },
    "type": [
      "RGB", 
      "NDIV"
    ],
    "weight": "0.198",
    "properties": {
      "video_modes": [
        "1920 x 1080 @ 24 fps",
        "1280 x 720 @ 30fps"
      ],
      "video_file_formats": [
        "H.264"
      ]
    }
  }
}
```

`PATCH /fleet/camera-providers/{camera_provider_id}/camera-models/{camera_model_id}`

This endpoint allows you to edit and update information regarding a `camera_model` that has already been created. For the request body of this endpoint, it is not necessary to pass in values for all the properties of a `camera_model`. All of the following properties are optional: 

| Property     | Type   | Description                                                                                        |
| ------------ | ------ | -------------------------------------------------------------------------------------------------- |
| `name`       | String | Name of the camera model                                                                           |
| `model_id`   | String | Camera model ID                                                                                    |
| `provider`   | Object | Object representing the camera provider. Contains the `name` of the provider and the `provider_id` |
| `weight`     | String | Weight of the camera in kilograms (kg)                                                             |
| `type`       | Array  | Array of enumerated strings describing the type of the camera. (see below)                         |
| `properties` | Object | Object representing the properties of this camera model. (see below)                               |

For more information on these properties, refer to the `camera_model` object description at the [beginning of this section](#camera-models)

A `camera_model` that has been successfully updated will return a response with a `"success": true` body and a `200 OK` status. Response body will also contain the updated `camera_model` object.

<div></div>

### Delete a camera model

> Code samples

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.delete 'https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models/{camera_model_id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.delete('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models/{camera_model_id}', params={

}, headers = headers)

print r.json()

```

```shell
curl -X DELETE 'https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models/{camera_model_id}' \
     -H 'Authorization: Bearer <AUTH_TOKEN>' \
     -H 'X-API-Key: <API_KEY>' \
```

```javascript
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://api.garuda.io/v2/fleet/camera-providers/{camera_provider_id}/camera-models/{camera_model_id}',
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
    "name": "Powershot S100",
    "model_id": "0e51493cd1ae85c097547de808642659",
    "provider": {
      "name": "Canon Inc.",
      "provider_id": "2db274b2709ce1ce89457057d6e9fd3b"
    },
    "type": [
      "RGB", 
      "NDIV"
    ]
  }
}
```

`DELETE /fleet/camera-providers/{camera_provider_id}/camera-models/{camera_model_id}`

Delete a specific camera model of a specific camera provider belonging to the company of the user.
