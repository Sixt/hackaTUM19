# hackaTUM Mobility API

This is an API that aggregates free floating vehicles, tier scooters, SIXT stations, parking spots, fuel stations and Taxis from the SIXT Go-orange platform.

## Questions?

Please ask your questions in the [TUM Discord server](https://discord.gg/5Jya86c).

# API Description

The API description gives you an overview of the available endpoints and what you can do with them.

## Base URL

`https://api.orange.sixt.com/v1/hackatum`

## Endpoints

### Endpoint 1: `/availability`

Returns all available products in a bounding box defined by the coordinates of the top left and bottom right corners. The maximum distance allowed is 10km.
You can use [bboxfinder.com](http://bboxfinder.com/#48.077161,11.476936,48.210947,11.653748) to create bounding boxes and get their coordinates.

#### Request
```
GET /v1/availability?tlLat={tlLat}&tlLon={tlLon}&brLat={brLat}&brLon={brLon}
```

##### Request parameters

| Field name        | Description | Data type | Required  |
|:------------------|:------------|:----------|:----------|
|`tlLat`| Top left latitude | float | true |
|`tlLon`| Top left longitude | float | true |
|`brLat`| Bottom right latitude | float | true |
|`brLon`| Bottom right latitude | float | true |


#### Response

<details>

<summary>Response Body</summary>

```javascript
{
  "vehicles": [
    {
      "id": "443969e2-4b16-4618-8cc9-00f4ee637bec",
      "make": "Make_VW",
      "model": "Model_VW:TOR",
      "bodyStyle": "BodyType_MM",
      "transmission": "Trans_A",
      "color": "Color_BLK",
      "imageUrl": "https://app.rental-images.sixt.com/rental-static/vehiclepicturews/741774220181122/BLK/1050x600/60.png",
      "position": {
        "latitude": 48.14258575439453,
        "longitude": 11.559269905090332
      },
      "seats": 7,
      "doors": 5,
      "primaryFuelTank": {
        "type": "FuelType_Gasoline",
        "percentage": 93
      },
      "power": 0
    }
  ],
  "stations": [
    {
      "id": "f6b315b6-a707-4155-a9e4-2ecc1a29dbf5",
      "position": {
        "latitude": 48.140032,
        "longitude": 11.566841
      }
    }
  ],
  "parkingSpots": [
    {
      "id": "77192ee3-edfd-4f0e-831d-f7ce90c067d8",
      "position": {
        "latitude": 48.35209961975642,
        "longitude": 11.788716316223145
      }
    }
  ],
  "taxis": [
    {
      "id": 30431,
      "position": {
        "latitude": 48.1343226,
        "longitude": 11.5739648
      }
    }
  ],
  "scooters": [
    {
      "id": "8003c29c-6a8c-47ea-bf5e-9d2ed5b21680",
      "range": 7,
      "position": {
        "latitude": 48.13559,
        "longitude": 11.573671
      },
      "batteryLevel": 25
    }
  ]
}
```
</details>

##### Response parameters

| Field name        | Description |
|:-----------       |:------------|
|`vehicles`         | array of free floating vehicles |
|`stations`         | array of car rental stations |
|`parkingSpots`     | array of free floating parking house |
|`taxis`            | array of nearby taxis |
|`scooters`         | array of free floating scooters |

#### Possible Status Codes

##### Success

| HTTP Status Code | Description |
|:-----------------|:------------|
|`200 OK` | the request has been processed |

##### Errors

| HTTP Status Code | Error Codes |
|:-----------------|-------------|
|`400 Bad Request` | bad parameters|
|`500 Internal Server Error` | something went wrong while getting the product |

## Example

Munich center: https://api.orange.sixt.com/v1/hackatum/availability?tlLat=48.149&tlLon=11.5589&brLat=48.133&brLon=11.582
