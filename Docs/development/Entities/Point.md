# Point

`Point` is the parent of all other entities and data in both **GoodWeatherFinder** and the **NWS API**. 

`Point` JSON is obtained via its GPS coordinates (latitude and longitude) via the following IRI:<br>
`GET: https://api.weather.gov/points/{latitude},{longitude}`

The following example is for Mt. Elbert, the highest peak in Colorado.<br>
`GET: https://api.weather.gov/points/39.1177,-106.4453`

## Primary Key
The primary key for `Point` is the IRI, included twice in the JSON: `id` and `properties.@id`.  
Both are stored in the entity as it may be helpful for verification later.

<table>
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java

public class Point {
	private String id; 
	private String propertiesId; 
}

```

</td>
<td>

```json

"id": "https://api.weather.gov/points/39.1177,-106.4453",
"properties": {
    "@id": "https://api.weather.gov/points/39.1177,-106.4453"
    
```

</td>
</tr>
</tbody>
</table>

## Relationships

| Related Entity | Owner | Relationship | Type |
| --- | --- | --- | -- |
| `Location` | `Location` | `Point` `1:1` `Location` | `Unidirectional` |
| `Geometry` | `Point` | `Point` `1:1` `Geometry` | `Unidirectional` |
| `Geometry`.`Coordinates` | `Point`.`Geometry` | `Geometry` `1:1` `Coordinates` | `Unidirectional` |
| `ForecastOffice` | `Point` | `Point` `1:1` `ForecastOffice` | `Unidirectional` |




<details>
<summary><h3>Location</h3></summary>

Each `Location` has one and only one `Point`. Each `Point` has one and only one `Location`.  
When `Point` is updated, it has no effect on `Location`.

```java

public class Point {
	private Location location;
}

```

</details>
<details>
<summary><h3>Geometry</h3></summary>

Each `Point` has at most one `Geometry`. That `Geometry` is unique to `Point`.  
When `Point` is updated, that `Geometry` is also updated.

The `Geometry` belonging to `Point` has at most one `Coordinates`.  
When `Geometry` is updated, `Coordinates` is also updated.

<table>
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java

public class Point {
	private Geometry geometry;
}

```

```java

public class Geometry {
	private String type;
	private List<Coordinate> coordinateList;
}

```

```java

public class Coordinates {
	private double latitude;
	private double longitude;
}

```

</td>
<td>

```json

"geometry": {
    "type": "Point",
    "coordinates": [
        -106.4453,
        39.117699999999999
    ]
}

```

</td>
</tr>
</tbody>
</table>

<details>
<summary>Click to show map of <code>Geometry</code> GeoJSON</summary>

```geojson

{
    "type": "Point",
    "coordinates": [
        -106.4453,
        39.117699999999999
    ]
}

```

</details>
</details>
<details>
<summary><h3>ForecastOffice</h3></summary>

Each `Point` has one and only one `ForecastOffice`.  That `ForecastOffice` has one or many `Point`.  
When `Point` is updated, `ForecastOffice` is also updated.

<table>
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java

public class Point {
	private ForecastOffice forecastOffice;
}

```

</td>
<td>

```json

"properties": {
	"forecastOffice": "https://api.weather.gov/offices/PUB"
}

```

</td>
</tr>
</tbody>
</table>

</details>
<details open>
<summary><h3>Forecast</h3></summary>

Each `Point` has two and only two `Forecast` - one normal and one hourly.  Each `Forecast` has one and only one `Point`.  
When `Point` is updated, each `Forecast` is also updated.

Each `Forecast` has one and only one `Geometry`. Each `Geometry` has one and only one `Forecast`.
When `Forecast` is updated, `Geometry` is also updated.

Each `Forecast` has either 14 (normal) or 156 (hourly) `Period`.  Each `Period` has one and only one `Forecast`.  
When `Forecast` is updated, each `Period` is also updated.

When `Point` is updated, a total of 2 `Forecast` and 170 `Period` are also updated.

<table>
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java

public class Point {
	private List<Forecast> forecastList;
}

```

```java

public class Forecast {
	private Geometry geometry;
	private List<Period> periodList;
}

```

```java

public class Coordinates {
	private double latitude;
	private double longitude;
}

```

</td>
<td>

##### Point

```json

"properties": {
	"forecast": "https://api.weather.gov/gridpoints/PUB/33,107/forecast",
	"forecastHourly": "https://api.weather.gov/gridpoints/PUB/33,107/forecast/hourly"
}

```

##### Forecast

```json

"geometry": {
    "type": "Polygon",
    "coordinates": [
        [
            [
                -106.4610958,
                39.117267400000003
            ],
            [
                -106.4586896,
                39.095231600000005
            ],
            [
                -106.4302713,
                39.097097800000007
            ],
            [
                -106.43267160000001,
                39.119133800000007
            ],
            [
                -106.4610958,
                39.117267400000003
            ]
        ]
    ]
},
"properties": {
	"periods": [
		{},
		{}
	]
}

```

</td>
</tr>
</tbody>
</table>

<details>
<summary>Click to show map of <code>`Forecast`.`Geometry`</code> GeoJSON</summary>

```geojson

{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "id": 1,
      "properties": {
        "ID": 0
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
              [-90,35],
              [-90,30],
              [-85,30],
              [-85,35],
              [-90,35]
          ]
        ]
      }
    }
  ]
}

```

</details>

</details>
<details open>
<summary><h3>ForecastGridData</h3></summary>


<table>
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java

public class Point {
	private ForecastGridData forecastGridData;
}

```

</td>
<td>

```json

"properties": {
	"forecastGridData": "https://api.weather.gov/gridpoints/PUB/33,107"
}

```

</td>
</tr>
</tbody>
</table>

</details>
<details open>
<summary><h3>ObservationStation</h3></summary>

<table>
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java

public class Point {
	private List<Forecast> forecastList;
}

```

</td>
<td>

```json

"properties": {
	"forecast": "https://api.weather.gov/gridpoints/PUB/33,107/forecast",
	"forecastHourly": "https://api.weather.gov/gridpoints/PUB/33,107/forecast/hourly"
}

```

</td>
</tr>
</tbody>
</table>

</details>
<details open>
<summary><h3>RelativeLocation</h3></summary>

<table>
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java

public class Point {
	private List<Forecast> forecastList;
}

```

</td>
<td>

```json

"properties": {
	"forecast": "https://api.weather.gov/gridpoints/PUB/33,107/forecast",
	"forecastHourly": "https://api.weather.gov/gridpoints/PUB/33,107/forecast/hourly"
}

```

</td>
</tr>
</tbody>
</table>

</details>
<details open>
<summary><h3>ForecastZone</h3></summary>

<table>
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java

public class Point {
	private List<Forecast> forecastList;
}

```

</td>
<td>

```json
"properties": {
	"forecast": "https://api.weather.gov/gridpoints/PUB/33,107/forecast",
	"forecastHourly": "https://api.weather.gov/gridpoints/PUB/33,107/forecast/hourly"
}
```

</td>
</tr>
</tbody>
</table>

</details>
<details open>
<summary><h3>County</h3></summary>

<table>
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java

public class Point {
	private List<Forecast> forecastList;
}

```

</td>
<td>

```json

"properties": {
	"forecast": "https://api.weather.gov/gridpoints/PUB/33,107/forecast",
	"forecastHourly": "https://api.weather.gov/gridpoints/PUB/33,107/forecast/hourly"
}

```

</td>
</tr>
</tbody>
</table>

</details>
<details open>
<summary><h3>FireWeatherZone</h3></summary>

<table>
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java

public class Point {
	private ForecastGridData forecastGridData;
}

```

</td>
<td>

```json

"properties": {
	"forecastGridData": "https://api.weather.gov/gridpoints/PUB/33,107"
}

```

</td>
</tr>
</tbody>
</table>

</details>

### Template

Each `Entity` has `Entity`. That `Entity` has `Entity.

<table>
<thead><tr>
<th>Java</th>
<th>JSON</th>
</thead></tr>
<tbody>
<tr>
<td>

```java

```
</td>
</tr>
<tr>
<td>

```json

```
</td>
</tr>
</tbody>
</table>









```java
public class Point {
	private String propertiesType; // corresponds to other types | used for verification later | i.e. wx:Point
}

public class RelativeLocation {
	private String type;
}
```


```json
"properties": {
	"@type": "wx:Point"
	
"geometry": {
    "type": "Point",
    "coordinates": [
        -106.4453,
        39.117699999999999
    ]
}
```
<hr>

```java
private String cwa; // County Warning Area | used in IRIs for forecastOffice, forecast, forecastGridData, observationStation
```

```json
"properties": {
	"cwa": "PUB"
```
<hr>

```java
private Geometry geometry; // single pair of Coordinates
```

```json
"geometry": {
    "type": "Point",
    "coordinates": [
        -106.4453,
        39.117699999999999
    ]
}
```
<hr>

```java

```

```json
"relativeLocation": {
    "type": "Feature",
    "geometry": {
        "type": "Point",
        "coordinates": [
            -106.318985,
            39.103709000000002
        ]
    },
    "properties": {
        "city": "Twin Lakes",
        "state": "CO",
        "distance": {
            "unitCode": "wmoUnit:m",
            "value": 11008.865990169001
        },
        "bearing": {
            "unitCode": "wmoUnit:degree_(angle)",
            "value": 278
        }
    }
}
```
<hr>

```java

```

```json

```
<hr>

```java

```

```json

```
<hr>

```java

```

```json

```
<hr>

| Property | JSON | Type | Description | Example |
| --- | --- | --- | --- | --- |
| `id` | `id`<br>`properties.@id` | `String` | `primary key`<br>`IRI` | `id = "https://api.weather.gov/points/39.1177,-106.4453";` |
| `type` | `type`<br>`properties.@type` | `String` | `GeoJSON @type` | `type = "Feature";`<br>`properties.@type = "wx:Point"` |
| `geometry` | `geometry` | `Geometry` | `Coordinates`  | `type = "Point";`<br>`coordinates = [-106.4453,39.117699999999999];` |
| properties.
<hr>

- id and properties.@id
	- IRI; primary key & id for this **point**
	- i.e. https://api.weather.gov/points/39.1177,-106.4453
- geometry.coordinates: single set of coordinates; the latitude and longitude for this point and what's used in the IPI (IPI is somewhat less precise)
- properties.cwa: County Warning Area; used in obtaining **forecast(s)**, **forecastGridData**, and **observationStations**

<details><summary><b>JSON</b> <i>Requested May 17 2022</i></summary>

```json
{
    "@context": [
        "https://geojson.org/geojson-ld/geojson-context.jsonld",
        {
            "@version": "1.1",
            "wx": "https://api.weather.gov/ontology#",
            "s": "https://schema.org/",
            "geo": "http://www.opengis.net/ont/geosparql#",
            "unit": "http://codes.wmo.int/common/unit/",
            "@vocab": "https://api.weather.gov/ontology#",
            "geometry": {
                "@id": "s:GeoCoordinates",
                "@type": "geo:wktLiteral"
            },
            "city": "s:addressLocality",
            "state": "s:addressRegion",
            "distance": {
                "@id": "s:Distance",
                "@type": "s:QuantitativeValue"
            },
            "bearing": {
                "@type": "s:QuantitativeValue"
            },
            "value": {
                "@id": "s:value"
            },
            "unitCode": {
                "@id": "s:unitCode",
                "@type": "@id"
            },
            "forecastOffice": {
                "@type": "@id"
            },
            "forecastGridData": {
                "@type": "@id"
            },
            "publicZone": {
                "@type": "@id"
            },
            "county": {
                "@type": "@id"
            }
        }
    ],
    "id": "https://api.weather.gov/points/39.1177,-106.4453",
    "type": "Feature",
    "geometry": {
        "type": "Point",
        "coordinates": [
            -106.4453,
            39.117699999999999
        ]
    },
    "properties": {
        "@id": "https://api.weather.gov/points/39.1177,-106.4453",
        "@type": "wx:Point",
        "cwa": "PUB",
        "forecastOffice": "https://api.weather.gov/offices/PUB",
        "gridId": "PUB",
        "gridX": 33,
        "gridY": 107,
        "forecast": "https://api.weather.gov/gridpoints/PUB/33,107/forecast",
        "forecastHourly": "https://api.weather.gov/gridpoints/PUB/33,107/forecast/hourly",
        "forecastGridData": "https://api.weather.gov/gridpoints/PUB/33,107",
        "observationStations": "https://api.weather.gov/gridpoints/PUB/33,107/stations",
        "relativeLocation": {
            "type": "Feature",
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -106.318985,
                    39.103709000000002
                ]
            },
            "properties": {
                "city": "Twin Lakes",
                "state": "CO",
                "distance": {
                    "unitCode": "wmoUnit:m",
                    "value": 11008.865990169001
                },
                "bearing": {
                    "unitCode": "wmoUnit:degree_(angle)",
                    "value": 278
                }
            }
        },
        "forecastZone": "https://api.weather.gov/zones/forecast/COZ060",
        "county": "https://api.weather.gov/zones/county/COC065",
        "fireWeatherZone": "https://api.weather.gov/zones/fire/COZ220",
        "timeZone": "America/Denver",
        "radarStation": "KGJX"
    }
}
```
</details>