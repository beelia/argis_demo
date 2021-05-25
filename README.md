# mobile_home_parks/{mhpid}

Get information about mobile home parks available for investment, including city, zip, street address, owner, size (acres), and apppraised value. `{mhpid}` refers to the ID for the park you might want to purchase. All mhpid codes are available from the Department of Homeland Security geographic information service (ArcGIS).

## Endpoint definition

`park_inventory/{mhpid}`

## HTTP method

<span class="label label-primary">GET</span>

## Parameters

| Parameter | Description | Data Type |
|-----------|------|----------|
| parks | *Optional*. The number of parks to include in the response. Default is 6. | integer |
| location | *Optional*. If you include the location, then only the zip will be returned in the response.| string |

## Sample request

```
curl -I -X GET
"https://api.mohome_parks.com/data/1.0/mobile_home_parks?zip=94043&appid=beekey&units=imperial&acreage=34"
```

## Sample response

```json
{
    "park_inventory": [
        {
            "mobile home park": "Mountain View, CA",
            "Santiago Villa": {
                "address": "1075 Space Park Way",
                "zip": 94043,
                "acres": 34,
                "units": 358,
                "value$": 22000000,
                "location": "near Googleplex"
                },
            "Sunset Estates": {
                "address": "433 Sylvan Ave.",
                "zip": 94041,
                "acres": 15.84,
                "units": 358,
                "value$": 10000000,
                "location": "off 237"
                },
            "New Frontier": {
                "address": "325 Sylvan Ave.",
                "zip": 94041,
                "acres": 12.8,
                "units": 358,
                "value$": 8000000,
                "location": "next to Sunset"
                },
            "location": "Mountain View",
            "Moffett MHP": {
                "address": "440 Moffett Blvd.",
                "zip": 94043,
                "acres": 12.1,
                "units": 358,
                "value$": 6000000,
                "location": "near NASA"
                },
            "Sahara Village": {
                "address": "191 E. El Camino Real",
                "zip": 94040,
                "acres": 14.36,
                "units": 358,
                "value$": 20000000,
                "location": "ECR and Grant"
                },
            "Moorpark": {
                "address": "501 Moorpark Way",
                "zip": 94041,
                "acres": 13.4,
                "units": 358,
                "value$": 11000000,
                "location": "near Central Xpwy"
            }
        }
    ]
}
```

The following table describes each item in the response.

|Response item | Description |
|----------|------------|
| **mobile home park** | The MHP ID for Mountain View parks - the official name in ArcGIS. |
| **{mhpid}** | The name of the mobile home park. |
| **{mhpid}/{address}** | The address of the mobile home park. |
| **{mhpid}/{zip}** | The zip code of the mobile home park. |
| **{mhpid}/{acres}** | The acreage of the mobile home park. |
| **{mhpid}/{units}** | The number of units in the mobile home park. |
| **{mhpid}/{value}** | The appraised value of the mobile home park in US dollars. |
| **{mhpid}/{location}** | The landmark location of the mobile home park. |

## Error and status codes

The following table lists the status and error codes related to this request.

| Status code | Meaning |
|--------|----------|
| 200 | Successful response |
| 400 | Bad request -- one or more of the parameters was rejected. |
| 4112 | The park was not found in the ArcGIS database. |
