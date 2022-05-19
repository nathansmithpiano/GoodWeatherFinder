# Location

Each `Location` is determined by a precise set of GPS coordinates (latitude and longitude).

> ### Development
> I began by listing data that may be relevant to a mountain summit.  Then, in the name of normalization, I reorganized that data into other entities.  `Location` and its other entities will all have their own tables in the database.

### Mt. Elbert

Mount Elbert is the highest peak in Colorado and a popular, well-known destination.  As the initial database contains Colorado peaks above 13,000 and 14,000 feet, I have chosen this location as the example for this documentation.

## Location

> **Legend:** **PK** = Primary Key | **NN** = Non Null | **AI** = Auto Incremented | **UQ** = Unique | **UN** = Unsigned


| Property | Type | Characteristics | Value |
| --- | --- | --- | --- |
| ID | `int` | PK, NN, AI, UQ, UN | generated |
| Name | `String` | NN, required | Mt. Elbert |
| `Category` | Entity (Collection) | NN, UN, required | Foreign Key `int` |
| `Geometry` | Entity (single) | NN, UN, required | Foreign Key `int` |
| `Mountain` | Entity (single) | optional | owned by `Mountain` |
| `Region` | Entity (Collection) | optional | Foreign Key `int` |
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
        <th>Geometry</th>
        <th>
            Coordinates
        </th>
    </tr>
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

### Region
<table>
    <tr>
        <th>ID</th>
        <th>parent_id</th>
        <th>Type</th>
        <th>Name</th>
    </tr>
    <tr>
        <td>1</td>
        <td>null</td>
        <td>Mountain Range</td>
        <td>Rocky Mountains</td>
    </tr>
    <tr>
        <td>2</td>
        <td>1</td>
        <td>Mountain Range</td>
        <td>Southern Rocky Mountains</td>
    </tr>
    <tr>
        <td>3</td>
        <td>2</td>
        <td>Mountain Range</td>
        <td>Sawatch</td>
    </tr>
    <tr>
        <td><b>4</b></td>
        <td><b>3</b></td>
        <td><b>Mountain Range</b></td>
        <td><b>Elbert Massif</b></td>
    </tr>
    <tr>
        <td><b>5</b></td>
        <td><b>null</b></td>
        <td><b>National Forest</b></td>
        <td><b>San Isabel National Forest</b></td>
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
