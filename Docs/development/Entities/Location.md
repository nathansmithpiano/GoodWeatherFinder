# Location

Each `Location` is determined by a precise set of GPS coordinates (latitude and longitude).

> ### Development
> I began by listing data that may be relevant to a mountain summit.  Then, in the name of normalization, I reorganized that data into other entities.  `Location` and its other entities will all have their own tables in the database.

### Mt. Elbert

Mount Elbert is the highest peak in Colorado and a popular, well-known destination.  As the initial database contains Colorado peaks above 13,000 and 14,000 feet, I have chosen this location as the example for this documentation.

### Location

| Property | Type | Characteristics | Value |
| --- | --- | --- | --- |
| ID | `int` | Primary Key, auto incremented, unique, unsigned | generated |
| Name | `String` | required, non-null | Mt. Elbert |
| `Type` | Entity (Collection) | required, non-null, unsigned | Foreign Key `int` |
| `Geometry` | Entity (single) | required, non-null, unsigned | Foreign Key `int` |
| `Mountain` | Entity (single) | optional | owned by `Mountain` |
| Country | United States |
| State | Colorado |
| County | Lake County, Colorado |
| Mountain Range | Rocky Mountains |
| Forest | San Isabel National Forest |
| Category | Mountain |
| Category | Summit |
| Category | Colorado 14er |
| Activity | Hiking |
| Activity | Climbing |
| Activity | Mountaineering |
| Activity | Trail Running |
| Activity | Camping |
| Activity | Backpacking |
| Activity | Skiing/Snowboarding (Backcountry) |

### Type

| Property | Type | Characteristics | Value |
| --- | --- | --- | --- |
| ID | `int` | Primary Key, auto incremented, unique, unsigned | generated |
| Name | `String` | required, non-null | Mountain Summit |

### Geometry

| Property | Type | Characteristics | Value |
| --- | --- | --- | --- |
| ID | `int` | Primary Key, auto incremented, unique, unsigned | generated |
| Type | `String` | required, non-null | Location |
| `Coordinate` | Entity (Collection) | required, non-null, unsigned | Foreign Key `int` |

### Coordinates

| Property | Type | Characteristics | Value |
| --- | --- | --- | --- |
| ID | `int` | Primary Key, auto incremented, unique, unsigned | generated |
| latitude | double | required, non-null | 39.118075 |
| longitude | double | required, non-null | -106.445417 |

### Mountain

| Property | Value |
| --- | --- |
| ID | `int` | Primary Key, auto incremented, unique, unsigned | generated |
| Name | `String` | required, non-null, unique | Mount Elbert |
| Abbreviation | `String` | required, non-null, unique | Mt. Elbert |
| `MountainRange` | Entity (single) | required, non-null | Foreign Key `int` |
| Elevation | `double` | required, non-null, unsigned | 4389.12 |
| Prominence |

### MountainRange

| Property | Value |
| --- | --- |
| Primary Key | TODO |

### MountainRange

| Property | Type | Characteristics | Value |
| --- | --- | --- | --- |
| ID | `int` | Primary Key, auto incremented, unique, unsigned | generated |
| Name | `String` | required, non-null, unique | Elbert Massif |
| Parent | `MountainRange` | --- | Foreign Key `int` |
| Name | `String` | required, non-null, unique | Rocky Mountains |
| Name | `String` | required, non-null, unique | Southern Rocky Mountains |
| Name | `String` | required, non-null, unique | Sawatch |
| Name | `String` | required, non-null, unique | Elbert Massif |
