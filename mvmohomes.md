# parks_for_sale/{mhpid}

Returns information about mobile home parks, including city, zip, street address, owner, size (acres), and apppraised value. 

`{mhpid}` refers to the ID for the park you want to look up. All mhpid codes are available from the Department of Homeland Security geographic information service (ArcGIS).

## Endpoint definition

`mohome_parks/{mhpid}`

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
"https://api.mohome_parks.com/data/1.0/parks_for_sale?zip=94043&appid=beekey&units=imperial&acreage=34"
```

## Sample response

```json
{
    "parks_for_sale": [
        {
            "location": "Mountain View",
            "Santiago Villa": {
                "1075 Space Park Way": {
                    "zip": 94043,
                    "acres": 34,
                    "units": 358,
                    "value$": 22000000,
                    "recommendation": "Great location"
                },
            "Sunset Estates": {
                "433 Sylvan Ave.": {
                    "zip": 94041,
                    "acres": 15.84,
                    "units": 358,
                    "value$": 22000000,
                    "recommendation": "Great location"
                },
            "New Frontier": {
                "325 Sylvan Ave.": {
                    "zip": 94041,
                    "acres": 12.8,
                    "units": 358,
                    "value$": 22000000,
                    "recommendation": "Great location"
                },
            "location": "Mountain View",
            "Moffett MHP": {
                "440 Moffett Blvd.": {
                    "zip": 94043,
                    "acres": 12.1,
                    "units": 358,
                    "value$": 22000000,
                    "recommendation": "Great location"
                },
            "Sahara Village": {
                "191 E. El Camino Real": {
                    "zip": 94040,
                    "acres": 14.36,
                    "units": 358,
                    "value$": 22000000,
                    "recommendation": "Great location"
                },
            "Moorpark": {
                "501 Moorpark Way": {
                    "zip": 94041,
                    "acres": 13.4,
                    "units": 358,
                    "value$": 22000000,
                    "recommendation": "Great location"
                }
            }
        }
    ]
}
```

The following table describes each item in the response.

|Response item | Description |
|----------|------------|
| **beach** | The beach you selected based on the beach ID in the request. The beach name is the official name as described in the National Park Service Geodatabase. |
| **{day}** | The day of the week selected. A maximum of 3 days gets returned in the response. |
| **{time}** | The time for the conditions. This item is included only if you include a time parameter in the request. |
| **{day}/{time}/tide** | The level of tide at the beach for a specific day and time. Tide is the distance inland that the water rises to, and can be a positive or negative number. When the tide is out, the number is negative. When the tide is in, the number is positive. The 0 point reflects the line when the tide is neither going in nor out but is in transition between the two states. |
| **{day}/{time}/wind** | The wind speed at the beach, measured in knots per hour or kilometers per hour depending on the units you specify. Wind affects the surf height and general wave conditions. Wind speeds of more than 15 knots per hour make surf conditions undesirable because the wind creates white caps and choppy waters. |
| **{day}/{time}/watertemp** | The temperature of the water, returned in Fahrenheit or Celsius depending upon the units you specify. Water temperatures below 70 F usually require you to wear a wetsuit. With temperatures below 60, you will need at least a 3mm wetsuit and preferably booties to stay warm.|
| **{day}/{time}/surfheight** | The height of the waves, returned in either feet or centimeters depending on the units you specify. A surf height of 3 feet is the minimum size needed for surfing. If the surf height exceeds 10 feet, it is not safe to surf. |
| **{day}/{time}/recommendation** | An overall recommendation based on a combination of the various factors (wind, watertemp, surfheight). Three responses are possible: (1) "Go surfing!", (2) "Surfing conditions are okay, not great," and (3) "Not a good day for surfing." Each of the three factors is scored with a maximum of 33.33 points, depending on the ideal for each element. The three elements are combined to form a percentage. 0% to 59% yields response 3, 60% - 80% and below yields response 2, and 81% to 100% yields response 1. |

## Error and status codes

The following table lists the status and error codes related to this request.

| Status code | Meaning |
|--------|----------|
| 200 | Successful response |
| 400 | Bad request -- one or more of the parameters was rejected. |
| 4112 | The beach ID was not found in the ArcGIS database. |

## Code example

The following code samples shows how to use the surfreport endpoint to get the surf height for a specific beach.

```html
<!DOCTYPE html>
<head>
<script src="https://code.jquery.com/jquery-2.1.1.min.js"></script>
<script>
var settings = {
  "async": true,
  "crossDomain": true,
  "url": "https://api.openweathermap.org/surfreport/25&days=1",
  "method": "GET"
}

$.ajax(settings).done(function (response) {
  console.log(response);
  $("#surfheight").append(response.surfreport.conditions);
});
</script>
</head>
<body>
<h2>Surf Height</h2>
<div id="surfheight"></div>
</body>
</html>
```

In this example, the `ajax` method from jQuery is used because it allows us to load a remote resource asynchronously.

In the request, you submit the authorization through a query string URL. The endpoint limits the days returned to 1 in order to increase the download speed.

For demonstration purposes, the response is assigned to the `response` argument of the `done` method, and then written out to the `surfheight` tag on the page.

We're just getting the surf height, but there's a lot of other data you could choose to display.
