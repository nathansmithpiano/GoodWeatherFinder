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
    <tr><h3>
        <th>Geometry</th>
        <th>
            Coordinates
        </th>
    </h3></tr>
    <tr>
        <td>
            <table>
                <tr>
                    <th>Type</th>
                    <th><code>Coordinates</code></th>
                </tr>
                <tr>
                    <td>Location</td>
                    <td><code>Coordinates</code></td>
            </table>
        </td>
        <td>
            <table>
                <tr>
                    <th>Latitude</th>
                    <th>Longitude</th>
                    <th><code>Geometry</code></th>
                </tr>
                <tr>
                    <td>39.118075</td>
                    <td>-106.445417</td>
                    <td><code>Geometry</code></td>
                </tr>
            </table>
        </td>
    </tr>
</table>

### TEMPLATE
<table>
    <tr>
        <th></th>
        <th></th>
    </tr>
    <tr>
        <td></td>
        <td></td>
    </tr>
</table>

### Mountain
<table>
    <tr>
        <th>Name</th>
        <th>Abbreviation</th>
        <th>Elevation</th>
        <th><code>MountainRange</code></th>
    </tr>
    <tr>
        <td>Mount Elbert</td>
        <td>Mt. Elbert</td>
        <td>4389.12</td>
        <td><code>MountainRange</code></td>
    </tr>
</table>

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
