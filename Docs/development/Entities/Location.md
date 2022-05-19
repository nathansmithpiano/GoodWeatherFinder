# Location

Each `Location` is determined by a precise set of GPS coordinates (latitude and longitude).

> ### Development
> I began by listing data that may be relevant to a mountain summit.  Then, in the name of normalization, I reorganized that data into other entities.  `Location` and its other entities will all have their own tables in the database.

### Mt. Elbert

Mount Elbert is the highest peak in Colorado and a popular, well-known destination.  As the initial database contains Colorado peaks above 13,000 and 14,000 feet, I have chosen this location as the example for this documentation.

### Location

> **Legend:** **PK** = Primary Key | **NN** = Non Null | **AI** = Auto Incremented | **UQ** = Unique | **UN** = Unsigned


| Property | Type | Characteristics | Value |
| --- | --- | --- | --- |
| ID | `int` | PK, NN, AI, UQ, UN | generated |
| Name | `String` | NN, required | Mt. Elbert |
| `Category` | Entity (Collection) | NN, UN, required | Foreign Key `int` |
| `Geometry` | Entity (single) | NN, UN, required | Foreign Key `int` |
| `Mountain` | Entity (single) | optional | owned by `Mountain` |
| Country | United States |
| State | Colorado |
| County | Lake County, Colorado |
| Mountain Range | Rocky Mountains |
| Forest | San Isabel National Forest |
| Activity | Hiking |
| Activity | Climbing |
| Activity | Mountaineering |
| Activity | Trail Running |
| Activity | Camping |
| Activity | Backpacking |
| Activity | Skiing/Snowboarding (Backcountry) |

### Category

| Name |
| --- |
| Mountain |
| Summit |
| Colorado 14er |

<table>
    <tr>
        <th>
            Geometry
        </th>
        <th>
            Coordinates
        </th>
    </tr>
    <tr>
        <td>
            <table>
                <tr>
                    <th>Type</th>
                    <th>`Coordinates`</th>
                </tr>
                <tr>
                    <td>Location</td>
                    <td>`Coordinates`</td>
            </table>
        </td>
        <td>
            <table>
                <tr>
                    <th>Latitude</th>
                    <th>Longitude</th>
                    <th>`Geometry`</th>
                </tr>
                <tr>
                    <td>39.118075</td>
                    <td>-106.445417</td>
                    <td>`Geometry`</td>
                </tr>
            </table>
        </td>
    </tr>
</table>

### Geometry

| Type | coordinate_id |
| --- | --- |
| Location | generated |

| Property | Type | Characteristics | Value |
| --- | --- | --- | --- |
| ID | `int` | PK, AI, UQ, UN | generated |
| Type | `String` | NN, required | Location |
| `Coordinate` | Entity (Collection) | NN, required, UN | Foreign Key `int` |

### Coordinates

| Property | Type | Characteristics | Value |
| --- | --- | --- | --- |
| ID | `int` | PK, AI, UQ, UN | generated |
| latitude | double | NN, required | 39.118075 |
| longitude | double | NN, required | -106.445417 |

### Mountain

| Property | Value |
| --- | --- |
| ID | `int` | PK, AI, UQ, UN | generated |
| Name | `String` | NN, UQ, required | Mount Elbert |
| Abbreviation | `String` | NN, UQ, required | Mt. Elbert |
| `MountainRange` | Entity (single) | NN, required | Foreign Key `int` |
| Elevation | `double` | NN, required, UN | 4389.12 |

### MountainRange

| Property | Type | Characteristics | Value |
| --- | --- | --- | --- |
| ID | `int` | PK, AI, UQ, UN | generated |
| Name | `String` | NN, UQ, required | Elbert Massif |
| Parent | `MountainRange` | optional | Foreign Key `int` |
| Name | `String` | NN, UQ, required | Rocky Mountains |
| Name | `String` | NN, UQ, required | Southern Rocky Mountains |
| Name | `String` | NN, UQ, required | Sawatch |
| Name | `String` | NN, UQ, required | Elbert Massif |
