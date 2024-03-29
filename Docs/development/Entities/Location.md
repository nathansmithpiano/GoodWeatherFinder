# Location

Each `Location` is determined by a precise set of GPS coordinates (latitude and longitude).

> ### Development
> I began by listing data that may be relevant to a mountain summit.  Then, in the name of normalization, I reorganized that data into other entities.  `Location` and its other entities will all have their own tables in the database.

### Mount Elbert

Mount Elbert is the highest peak in Colorado and a popular, well-known destination.  As the initial database contains Colorado peaks above 13,000 and 14,000 feet, I have chosen this location as the example for this documentation.

## Location Entity

> **Legend:
> ** **PK** = Primary Key | **FK** = Foreign Key | **NN** = Non Null | **AI** = Auto Incremented | **UQ** = Unique | **UN** = Unsigned

<table>
    <tr>
        <th>Property</th>
        <th>Type</th>
        <th>Characteristics</th>
        <th>Value</th>
        <th>Mapping</th>
    </tr>
    <tr>
        <td><a href="#locationid">id</a></td>
        <td><code>int</code></td>
        <td>PK, NN, AI, UQ, UN, required</td>
        <td>generated</td>
        <td></td>
    </tr>
    <tr>
        <td><a href="#locationname">name</a></td>
        <td><code>String</code></td>
        <td>NN, UQ, required</td>
        <td>Mount Elbert</td>
        <td></td>
    </tr>
    <tr>
        <td><a href="#locationelevation">elevation</a></td>
        <td><code>Double</code></td>
        <td>UN, optional</td>
        <td>4389.12</td>
        <td></td>
    </tr>
    <tr>
        <td><a href="#locationnicknames">nicknames</a></td>
        <td>List<<code>Name</code>></td>
        <td>optional</td>
        <td>
            <code>Name</code>, ...
            <br>
            <code>Name</code>
        </td>
        <td>
            <code>Location></code>
            <code>m:m></code>
            <code>Name></code>
            <br>
            <code>join table</code>
        </td>
    </tr>
    <tr>
        <td><a href="#locationgeometry_id">geometry<br>(geometry_id)</a></td>
        <td><code>Geometry</code></td>
        <td>FK, NN, UN, required</td>
        <td><code>Geometry</code></td>
        <td>
            <code>Location</code>
            <code>m:1</code>
            <code>Geometry</code>
            <br>
            <code>location.geometry_id</code>
            <code>int</code>
        </td>
    </tr>
    <tr>
        <td><a href="#locationcategories">categories</a></td>
        <td>List<<code>Category</code>></td>
        <td>optional</td>
        <td>
            <code>Category</code>, ...
            <br>
            <code>Category</code>
        </td>
        <td>
            <code>Location</code>
            <code>m:m</code>
            <code>Category</code>
            <br>
            <code>join table</code>
        </td>
    </tr>
    <tr>
        <td><a href="#locationregions">regions</a></td>
        <td>List<<code>Region</code>></td>
        <td>optional</td>
        <td>
            <code>Region</code>, ...
            <br>
            <code>Region</code>
        </td>
        <td>
            <code>Location</code>
            <code>m:m</code>
            <code>Region</code>
            <br>
            <code>join table</code>
        </td>
    </tr>
    <tr>
        <td><a href="#locationactivities">activities</a></td>
        <td>List<<code>Activity</code>></td>
        <td>optional</td>
        <td>
            <code>Activity</code>, ...
            <br>
            <code>Activity</code>
        </td>
        <td>
            <code>Location</code>
            <code>m:m</code>
            <code>Activity</code>
            <br>
            <code>join table</code>
        </td>
    </tr>
</table>
<hr>

## <a href="#location-entity">location.id</a><small>
💡 Click on the blue headers to return to the Entity table
- Primary Key for `Location`. Automatically generated by the database.  
- **Non-null**, **auto-increment**, **unique**, **unsigned**, and **required**.
<hr>

## <a href="#location-entity">location.name</a>
- Name for this location.
- Each location has one primary name.  This primary name is unique for all Locations.
- This should be unique including all nicknames to prevent confusion.
    - [ ] `Location.name` should not exist in `Nickname.name`.
    - OR, should a `Location.name` be allowed to be non-unique, and `Region`, `Category`, or `Activity` further distinguishes?  Seems confusing.
- **Non-null**, **unique**, and **required**.

```java
public class Location {
    private int id;
    private String name;
}
```

### Merged `Location`

<table> <!-- Location Merged -->
    <tr>
        <th><code>Location</code><br>id</th>
        <th><code>Location</code><br>name</th>
    </tr>
    <tr>
        <td>1</td>
        <td>Mount Elbert</td>
    </tr>
</table>
<hr>

## <a href="#location-entity">location.nicknames</a>
- Additional names for this location.
    - For example, Mount Elbert is also known as Mt. Elbert. It may also have a traditional name, names in other languages, nicknames, etc.
    - `Location.name` corresponds to its primary name.  
    - The join table links a `Location` with its `nicknames`.
        - - [ ] Use business logic to prevent a user from setting its `Location.name` within its `List<Name> nicknames`.
- While primary name must be unique, other names are not.  Many `Location` may share the same `Nickname.name` in their `List<Name> nicknames`.
    - For example, several `Location` may be called "Buffalo Mountain", but each `Location` would have a unique primary name of "Buffalo Mountain A", "Buffalo Mountain (CO)", etc.  
    - If "Buffalo Mountain A" was deleted, we do not want all "Buffalo Mountain" records in the `Nickname` table to be deleted from the database.
    - If no records exist in the join table connecting a `Location` with "Buffalo Mountain", within `Nickname`, "Buffalo Mountain" should be deleted.
        - This seems possible via `orphanRemoval = true` on the `Location` side
            - - [ ] confirm via JUnit5 tests
    - Therefore, the database would have several copies of the "Buffalo Mountain" `Nickname`.
- For `Location.nicknames`, **`Location` `1:m` `Nickname`**.
- **Unidirectional**, `Location` is **owner**.
    - `Nickname` does not need to know about its `Location`, `Region`, or other relationships.
    - A `m:m` relationship between `Location` and `Nickname` would allow for proper normalization and would prevent duplicates, but this would require manual deleting and seems excessive for this application.
    - Also, other entities, such as `Region`, may also use the `Nickname` table for a collection of names.
- **Optional** - a location may only have one name and `List<Nickname> nicknames` may be empty or **null**.

<table>
<tr>
    <!-- Top row headers -->
    <th colspan="2">Location</th>
    <th>Join Table</th>
</tr>
<tr>
<!-- Location Code -->
<td>

```java
public class Location {
    private int id;
    private String name;

    @OneToMany
    @JoinTable(
        name = "location_nicknames",
        joinColumns = @JoinColumn(name = "location_id"),
        inverseJoinColumns = @JoinColumn(name = "name_id") )
    private List<Name> nicknames;
}
```

</td>
<!-- Location Table -->
<td>
    <table>
        <tr>        
            <th>id</th>
            <th>name</th>
        </tr>
        <tr>
            <td>1</td>
            <td>Mount Elbert</td>
        </tr>
    </table>
</td>
<!-- Join Table -->
<td rowspan="3">
    <table>
        <tr>        
            <th>location_id</th>
            <th>name_id</th>
        </tr>
        <tr>
            <td>1</td>
            <td>3</td>
        </tr>
        <tr>
            <td>1</td>
            <td>4</td>
        </tr>
        <tr>
            <td>1</td>
            <td>5</td>
        </tr>
    </table>

<!-- Join Table message -->
- [x] A `Location`'s primary name  
(`Location.name`) should not  
be used within any  
`Location.nicknames`

</td>

<!-- Name Header -->
<tr>
    <th colspan="2">Name</th>
</tr>
<tr>
<!-- Name Code -->
<td>

```java
public class Name {
    private int id;
    private String name;
}
```

</td>
<!-- Name Table -->
<td>
    <table>
        <tr>        
            <th>id</th>
            <th>name</th>
        </tr>
        <tr>
            <td>3</td>
            <td>Mt. Elbert</td>
        </tr>
        <tr>
            <td>4</td>
            <td>Other Nickname</td>
        </tr>
        <tr>
            <td>5</td>
            <td>Traditional Name</td>
        </tr>
    </table>
</td>
</tr>
</table>

### Merged `Location`

<table><!-- Location Merged -->
    <tr>
        <th><code>Location</code><br>id</th>
        <th><code>Location</code><br>name</th>
        <th><code>Join Table</code><br>location_id</th>
        <th><code>Join Table</code><br>name_id</th>
        <th><code>Name</code><br>name</th>
        <th><code>Location</code><br>nicknames</th>
    </tr>
    <tr>
        <td rowspan="3">1</td>
        <td rowspan="3">Mount Elbert</td>
        <td>1</td>
        <td>3</td>
        <td>Mt. Elbert</td>
        <td rowspan="3">
            [ "Mt. Elbert",<br>
            "Other Nickname",<br>
            "Traditional Name" ]
        </td>
    </tr>
    <tr>
        <td>1</td>
        <td>4</td>
        <td>Other Nickname</td>
    </tr>
    <tr>
        <td>1</td>
        <td>5</td>
        <td>Traditional Name</td>
    </tr>
</table>


## <a href="#location-entity">location.elevation</a>
- Elevation for this location, in meters.
- **Optional** - relevant for some locations but not others. May be **null**.
    - i.e. elevation is important for a mountain summit but not for a beach

<table>
<!-- Header -->
<tr>
    <th colspan="2">Location</th>
</tr>
<tr>
<!-- Location Code -->
<td>

```java
public class Location {
    private int id;
    private Double elevation;
}
```

</td>
<!-- Location Table -->
<td>
    <table>
        <tr>        
            <th>id</th>
            <th>name</th>
            <th>elevation</th>
        </tr>
        <tr>
            <td>1</td>
            <td>Mount Elbert</td>
            <td>4389.12</td>
        </tr>
    </table>
</td>
</tr>
</table>


## <a href="#location-entity">location.geometry_id</a>
- Foreign key for this location's geometry.
- `@JoinColumn` via `location.geometry_id`.
- `Geometry` contains a coordinateList, which for a `Location` contains one and only one `Coordinates`.
    - `Location` does not directly relate to `Coordinates` as `Geometry.type` is necessary when producing maps via [leafly](https://www.leafly.com/).
    - For other entities, such as `RelativeLocation`, a `Geometry` has many `Coordinates`.
    - For `Geometry` and `Coordinate`, `@JoinColumn` via `coordinates.geometry_id`.
- Special considerations:
    - `Location` cannot obtain any weather data without `Coordinates`, so `location.geometry_id` is required.
    - No two locations should share the same coordinates, so for `location.geometry_id` should be unique.
    - Users could attempt to add a `Location` with `Coordinates` lacking precision, i.e. 39, -106. Before submitting a new location, it is necessary to confirm the `Coordinates` are unique and to re-prompt.
        - When submitting a location, a map could appear to confirm the location, and a user could drag the point to correct precision.  From the map, more precise `Coordinates` could be obtained.
- **Unidirectional**, `Geometry` is **owner**.
    - `Coordinates` does not need to know about its `Geometry`.
    - **`Geometry` `1:m` `Coordinates`**.
- **Non-null**, **unique**, and **required**.

<table>
<tr>
    <!-- Location Header -->
    <th colspan="2">Location</th>
</tr>
<tr>

<!-- Location Code -->
<td>

```java
public class Location {
    @OneToOne
    @JoinColumn(name = "geometry_id")
    private Geometry geometry;
}
```

</td>
<td>
    <!-- Location Table -->
    <table>
        <tr>
            <th>id</th>
            <th>name</th>
            <th>geometry_id</th>
        </tr>
        <tr>
            <td>1</td>
            <td>Mount Elbert</td>
            <td>2</td>
        </tr>
    </table>
</td>
</tr>

<tr>
    <!-- Geometry Header -->
    <th colspan="2">Geometry</th>
</tr>
<tr>
<!-- Geometry Code -->
<td>

```java
public class Geometry {
    @OneToMany(mappedBy = "geometry")
    private List<Coordinates> coordinates;
}
```

</td>
<td>
    <!-- Geometry Table -->
    <table>
        <tr>
            <th>id</th>
            <th>Type</th>
        </tr>
        <tr>
            <td>2</td>
            <td>Point</td>
        </tr>
    </table>
</td>
</tr>

<tr>
    <!-- Coordinates Header -->
    <th colspan="2">Coordinates</th>
</tr>
<tr>
<!-- Coordinates Code -->
<td>

```java
public class Coordinates {
    @ManyToOne
    @JoinColumn(name = "geometry_id")
    private Geometry geometry;
}
```

</td>
<td>
    <!-- Coordinates Table -->
    <table>
        <tr>
            <th>id</th>
            <th>geometry_id</th>
            <th>Latitude</th>
            <th>Longitude</th>
        </tr>
        <tr>   
            <td>3</td>
            <td>2</td>
            <td>39.118075</td>
            <td>-106.445417</td>
        </tr>
    </table>
</td>
</tr>
</table>

### Merged `Location`

<table><!-- Location Merged -->
    <tr>
        <th><code>Location</code><br><code>Name</code></th>
        <th><code>Geometry</code><br>id</th>
        <th><code>Geometry</code><br>type</th>
        <th><code>Coordinates</code><br>id</th>
        <th><code>Coordinates</code><br>geometry_id</th>
        <th><code>Coordinates</code><br>latitude</th>
        <th><code>Coordinates</code><br>longitude</th>
    </tr>
    <tr>
        <td>Mount Elbert</td>
        <td>2</td>
        <td>Point</td>
        <td>3</td>
        <td>2</td>
        <td>39.118075</td>
        <td>-106.445417</td>
    </tr>
</table>


## <a href="#location-entity">location.categories</a>

- `Category` is a generic way to organize locations.
- Rather than having different tables for `Mountain`, `Trailhead`, `Parking Lot`, `Lake`, `Beach` etc, `Category` provides a way to group these things together.
- Each `Category` is set at a high level and unlikely to be deleted.  An administrator may update or perhaps remove a `Category`, but this would be rare.
- `Region` also uses `Category` in the same way.
    - As `Category` is used by multiple other entities, `Category` is given a property `String` of `Category.appliesTo`, which matches with the name of the entity the category applies to.
    - A `Category` with the same name may exist if its `appliesTo` for a different entity. Duplicates should not exist for both properties.
- While it would be possible to make `Category` optional, this could lead to confusion, especially as the data scales, so for business reasons, `Category` is **required**.
- **Unidirectional**, `Location` is **owner**.
    - `Category` does not need to know about the entities which use it.
    - Seperate join tables are necessary.
        - **`Location` `m:m` `Category`**

<table>
    <tr>
        <!-- Table Headers -->
        <th colspan="2">Location</th>
        <th>Join Table</th>
    </tr>
    <tr>
<!-- Location Code -->
<td>

```java
public class Location {
    private int id;
    private List<Category> categories;
}
```

</td>
        <td>
            <!-- Location Table -->
            <table>
                <tr>
                    <th>id</th>
                    <th>name</th>
                </tr>
                <tr>
                    <td>1</td>
                    <td>Mount Elbert</td>
                </tr>
            </table>
        </td>
        <td rowspan="3">
            <!-- Join Table -->
            <table>
                <tr>
                    <th>location_id</th>
                    <th>category_id</th>
                </tr>
                <tr>
                    <td>1</td>
                    <td>2</td>
                </tr>
                <tr>
                    <td>1</td>
                    <td>3</td>
                </tr>
                <tr>
                    <td>1</td>
                    <td>4</td>
                </tr>
            </table>
        </td>
    </tr>

<tr>
    <!-- Category Header -->
    <th colspan="2">Category</th>
</tr>
<tr>
<!-- Category Code -->
<td>

```java
public class Category {
    private int id;
    private String name;
}
```

</td>
<td>
    <!-- Category Table -->
    <table>
        <tr>
            <th>id</th>
            <th>name</th>
            <th>applies_to</th>
        </tr>
        <tr>
            <td>2</td>
            <td>Mountain</td>
            <td>Location</td>
        </tr>
        <tr>
            <td>3</td>
            <td>Summit</td>
            <td>Location</td>
        </tr>
        <tr>
            <td>4</td>
            <td>Colorado 14er</td>
            <td>Location</td>
        </tr>
    </table>
</td>
</tr>
</table>

### Merged `Location`

<table><!-- Location Merged -->
    <tr>
        <th><code>Location</code><br>id</th>
        <th><code>Location</code><br><code>Name</code></th>
        <th><code>Join Table</code><br>location_id</th>
        <th><code>Join Table</code><br>category_id</th>
        <th><code>Category</code><br>name</th>
        <th><code>Location</code><br>categories</th>
    </tr>
    <tr>
        <td rowspan="3">1</td>
        <td rowspan="3">Mount Elbert</td>
        <td>1</td>
        <td>2</td>
        <td>Mountain</td>
        <td rowspan="3">Mountain, Summit, Colorado 14er</td>
    </tr>
    <tr>
        <td>1</td>
        <td>3</td>
        <td>Summit</td>
    </tr>
    <tr>
        <td>1</td>
        <td>4</td>
        <td>Colorado 14er</td>
    </tr>
</table>


## <a href="#location-entity">location.regions</a>
- `Region` is a way of grouping locations based on geographical characteristics.
- Each `Location` can have one or many `Region`.
    - Mount Elbert is part of the Elbert Massif, Sawatch Range, Southern Rocky Mountains, Rocky Mountains, and Colorado.
- A mountain like Mount Elbert has one primary Mountain Range, and that Mountain Range has several parent ranges.
    - Example of parent/child relationships in `Region`:
        - The *Elbert Massif* is a child of the *Sawatch* range.
        - The *Sawatch* range is a child of *Southern Rocky Mountains*.
        - *Southern Rocky Mountains* is a child of the *Rocky Mountains*.
        - Some of these are in the *Colorado* `Region`.
            - Some of these `Region` are in the `Category` *Mountain Range*, while *Colorado* is in the `Category` *State*.  To determine all the mountain summits in Colorado, a user would search `Location``Category` of *Summit* and `Region``State` of *Colorado*.
    - Unlike `Category`, hierarchy is important for `Region`.
        - For example, a user may want to consider other locations nearby, or they may be interested in a more broad area.
        - *Rocky Mountains (CO)* would contain many thousands of locations, while *Elbert Massif* would only contain a dozen or so. A parent contains all of its children.
            - [ ] Enable searching all children of a `Region` by aggregating all successive parents, with or without additional parameters like `Category`.
    - A `Location` could be attached to several different geographical groupings.  Rather than having an ever-expanding number of tables with very similar data, each `Region` is given one `Category`.
        - A `Region``Category` would be set at a high level and unlikely to change at the user level.  Unlike with other entities, i.e. `Location.nicknames`, it is unlikely that a `Region``Category` would ever be deleted.
        - Each `Location` can have many `Region` in its `location.regions`, but should only have one of each `Category` for `Region`.
            - For example, Mount Elbert is assigned the *Elbert Massif*, not all of the parent ranges.  The `Region` itself has a parent, which has a parent, and so on.
            - [ ] Assure that a location has at most one of each `Region``Category` in its `location.regions`.
            - [ ] Only display the `Region` for each `Region``Category`, and display nothing about that `Region``Category` if `Location.regions` for that `Region``Category` is empty or null.
- Like `Location`, `Region` has one primary name and a collection of `Region.nicknames`.
    - Limiting a `Location`, `Region`, or other entities to only one name would reduce the ability to search - in the application, other resources, search engines, and so on. This also allows for multi-language data and searching.
- Relationships will be the same as `Location``Nickname` and `Location``Category`.
    - Join tables `region_category` and `region_nickname`.
    - As in the above example for `Location` "Buffalo Mountain", duplicate `Nickname.name` and `Category.name` may exist.
        - - [ ] verify orphan removal via JUnit5 tests
- **`Location` `m:m` `Region`**
    - Join table `location_region`.
    - `Location` can only have one of each `Region``Category`.
        - Build this within the application rather than database structure.
- For `Region.category`, **`Region` `1:1` `Category`**.
    - For both, **Unidirectional**, `Region` is **owner**.
    - Join table `region_category`.
    - **Required**
- For `Region.nicknames`, **`Region` `1:m` `Nickname`**.
    - **Unidirectional**, `Region` is **owner**.
    - **Optional**

<table>
    <tr>
        <!-- Table Headers -->
        <th colspan="2">Region</th>
        <th>Join Table</th>
    </tr>
    <tr>
<!-- Region Code -->
<td>

```java
public class Region {
    private int id;
    private String name;
    private Region parent;
    private List<Name> nicknames;
}
```

</td>
        <td>
            <!-- Region Table -->
            <table>
                <tr>
                    <th>id</th>
                    <th>parent_id</th>
                    <th>name_id</th>
                </tr>
                <tr>
                    <td>1</td>
                    <td></td>
                    <td>Rocky Mountains</td>
                </tr>
                <tr>
                    <td>2</td>
                    <td>1</td>
                    <td>Southern Rocky Mountains</td>
                </tr>
                <tr>
                    <td>3</td>
                    <td>2</td>
                    <td>Sawatch</td>
                </tr>
                <tr>
                    <td>4</td>
                    <td>3</td>
                    <td>Elbert Massif</td>
                </tr>
                <tr>
                    <td>5</td>
                    <td></td>
                    <td>San Isabel National Forest</td>
                </tr>
                <tr>
                    <td>6</td>
                    <td>5</td>
                    <td>Colorado</td>
                </tr>
                <tr>
                    <td>7</td>
                    <td></td>
                    <td>United States</td>
                </tr>
            </table>
        </td>
        <td>
            <!-- Join Table region_name -->
            <table>
                <tr>
                    <th>region_id</th>
                    <th>nickname_id</th>
                </tr>
                <tr>
                    <td>4</td>
                    <td>11</td>
                </tr>
                <tr>
                    <td>4</td>
                    <td>12</td>
                </tr>
                <tr>
                    <td>6</td>
                    <td>15</td>
                </tr>
                <tr>
                    <td>7</td>
                    <td>16</td>
                </tr>
            </table>
        </td>
    </tr>

<tr>
    <!-- Name Header -->
    <th colspan="2">Nickname</th>
    <th>Join Table</th>

</tr>
<tr>
<!-- Name Code -->
<td>

```java
public class Nickname {
    private int id;
    private String name;
}
```

</td>
<td>
    <!-- Name Table -->
    <table>
        <tr>
            <th>id</th>
            <th>name</th>
        </tr>
        <tr>
            <td>13</td>
            <td>EM 1</td>
        </tr>
        <tr>
            <td>14</td>
            <td>EM 2</td>
        </tr>
        <tr>
            <td>15</td>
            <td>CO</td>
        </tr>
        <tr>
            <td>15</td>
            <td>USA</td>
        </tr>
    </table>
</td>
<td rowspan="3">
    <!-- Join Table region_category -->
    <table>
        <tr>
            <th>region_id</th>
            <th>category_id</th>
        </tr>
        <tr>
            <td>1</td>
            <td>11</td>
        </tr>
        <tr>
            <td>2</td>
            <td>11</td>
        </tr>
        <tr>
            <td>3</td>
            <td>11</td>
        </tr>
        <tr>
            <td>4</td>
            <td>11</td>
        </tr>
        <tr>
            <td>5</td>
            <td>12</td>
        </tr>
        <tr>
            <td>6</td>
            <td>13</td>
        </tr>
        <tr>
            <td>7</td>
            <td>14</td>
        </tr>
    </table>
</td>
</tr>
<tr>
    <!-- Category Header -->
    <th colspan="2">Category</th>
</tr>
<tr>
<!-- Category Code -->
<td>

```java
public class Category {
    private int id;
    private String name;
}
```

</td>
<td>
    <!-- Category Table -->
    <table>
        <tr>
            <th>id</th>
            <th>name</th>
            <th>applies_to</th>
        </tr>
        <tr>
            <td>11</td>
            <td>Mountain Range</td>
            <td>"Region"</td>
        </tr>
        <tr>
            <td>12</td>
            <td>National Forest</td>
            <td>"Region"</td>
        </tr>
        <tr>
            <td>13</td>
            <td>State</td>
            <td>"Region"</td>
        </tr>
        <tr>
            <td>14</td>
            <td>Country</td>
            <td>"Region"</td>
        </tr>
    </table>
</td>
</tr>
</table>

<table>
    <!-- Location Merged -->
    <tr>
        <th>Merged <code>Location</code></th>
    </tr>
    <tr>
        <td>
            <table>
                <tr>
                    <th><code>Location</code><br>name</th>
                    <th><code>Region</code><br>id</th>
                    <th><code>Region</code><br>name</th>
                    <th><code>Region</code><br>parent</th>
                    <th><code>Region</code><br>category</th>
                </tr>
                <tr>
                    <td rowspan="4">Mount Elbert</td>
                    <td>4</td>
                    <td>Elbert Massif</td>
                    <td>Sawatch</td>
                    <td>Mountain Range</td>
                </tr>
                <tr>
                <td>5</td>
                    <td>San Isabel National Forest</td>
                    <td>null</td>
                    <td>National Forest</td>
                </tr>
                <tr>
                    <td>6</td>
                    <td>Colorado</td>
                    <td>United States</td>
                    <td>State</td>
                </tr>
            </table>
        </td>
    </tr>
</table>


<table>
    <tr><th>Merged <code>Region</code></th></tr>
    <tr>
        <td>
            <table>
                <tr>
                    <th>id</th>
                    <th>name</th>
                    <th>nicknames</th>
                    <th>Parent</th>
                    <th>Category</th>
                </tr>
                <tr>
                    <td>1</td>
                    <td>Rocky Mountains</td>
                    <td></td>
                    <td></td>
                    <td>Mountain Range</td>
                </tr>
                <tr>
                    <td>2</td>
                    <td>Southern Rocky Mountains</td>
                    <td></td>
                    <td>Rocky Mountains</td>
                    <td>Mountain Range</td>
                </tr>
                <tr>
                    <td>3</td>
                    <td>Sawatch</td>
                    <td></td>
                    <td>Southern Rocky Mountains</td>
                    <td>Mountain Range</td>
                </tr>
                <tr>
                    <td>4</td>
                    <td>Elbert Massif</td>
                    <td>EM 1, EM 2</td>
                    <td>Sawatch</td>
                    <td>Mountain Range</td>
                </tr>
                <tr>
                    <td>5</td>
                    <td>San Isabel National Forest</td>
                    <td></td>
                    <td></td>
                    <td>National Forest</td>
                </tr>
                <tr>
                    <td>6</td>
                    <td>Colorado</td>
                    <td>CO</td>
                    <td>United States</td>
                    <td>State</td>
                </tr>
                <tr>
                    <td>7</td>
                    <td>United States</td>
                    <td>USA</td>
                    <td></td>
                    <td>Country</td>
                </tr>
            </table>
        </td>
    </tr>
</table>


## <a href="#location-entity">location.activities</a>
- Each `Location` can be associated with one or many `Activities`.
- For example, Mount Elbert is popular for hiking, backpacking, camping, backcountry skiing, running, and many other activities.  A user may want to search for many locations by activity.
- Similar to other entities, `Activity` has one primary name and can have nicknames.
    - Example: *Touring* may also be called *Skiing, Off Piste* and/or *Skiing/Snowboarding (Backcountry)*.
- for `Activity.nicknames`, **`Activity` `1:m` `Nickname`**.
    - **Unidirectional**, `Activity` is **owner**.
    - **Optional**
- ** `Location` `m:m` `Activity`**
    - Join table `location_activity`.
    - **Unidirectional**, `Location` is **owner**.
    - **Required**

<table>
    <tr>
        <th colspan="2">Location</th>
        <th>Join Table</th>
    </tr>
    <tr>
<td>

```java
public class Location {
    private int id;
    private String name;
    private List<Activity> activities;
}
```

</td>
        <td>
            <table>
                <tr>
                    <th>id</th>
                    <th>name</th>
                </tr>
                <tr>
                    <td>1</td>
                    <td>Mount Elbert</td>
                </tr>
            </table>
        </td>
        <td rowspan="3">
            <table>
                <tr>
                    <th>location_id</th>
                    <th>activity_id</th>
                </tr>
                <tr>
                    <td>1</td>
                    <td>2</td>
                </tr>
                <tr>
                    <td>1</td>
                    <td>3</td>
                </tr>
                <tr>
                    <td>1</td>
                    <td>4</td>
                </tr>
                <tr>
                    <td>1</td>
                    <td>5</td>
                </tr>
                <tr>
                    <td>1</td>
                    <td>6</td>
                </tr>
                <tr>
                    <td>1</td>
                    <td>7</td>
                </tr>
                <tr>
                    <td>1</td>
                    <td>8</td>
                </tr>
            </table>
        </td>
    </tr>

<tr>
    <th colspan="2">Activity</th>
</tr>
<tr>
<td>

```java
public class Activity {
    private int id;
    private String name;
    private List<Name> nicknames;
}
```

</td>
<td>
    <table>
        <tr>
            <th>id</th>
            <th>name</th>
        </tr>
        <tr>
            <td>2</td>
            <td>Hiking</td>
        </tr>
        <tr>
            <td>3</td>
            <td>Climbing</td>
        </tr>
        <tr>
            <td>4</td>
            <td>Mountaineering</td>
        </tr>
        <tr>
            <td>5</td>
            <td>Trail Running</td>
        </tr>
        <tr>
            <td>6</td>
            <td>Camping</td>
        </tr>
        <tr>
            <td>7</td>
            <td>Backpacking</td>
        </tr>
        <tr>
            <td>8</td>
            <td>Touring</td>
        </tr>
    </table>
</td>
</tr>
<tr>
    <th colspan="2">Name</th>
    <th>Join Table</th>
</tr>
<tr>
<td>

```java
public class Name {
    private int id;
    private String name;
}
```

</td>
    <td>
        <table>
            <tr>
                <th>id</th>
                <th>name</th>
            </tr>
            <tr>
                <td>19</td>
                <td>Skiing/Snowboarding (Backcountry)</td>
            </tr>
            <tr>
                <td>20</td>
                <td>Skiing, Off Piste</td>
            </tr>
        </table>
    </td>
    <td>
        <table>
            <tr>
                <th>activity_id</th>
                <th>name_id</th>
            </tr>
            <tr>
                <td>8</td>
                <td>19</td>
            </tr>
            <tr>
                <td>8</td>
                <td>20</td>
            </tr>
        </table>
    </td>
</tr>
</table>

<table>
    <!-- Location Merged -->
    <tr>
        <th>Merged <code>Location</code> and <code>Activity</code></th>
    </tr>
    <tr>
        <td>
            <table>
                <tr>
                    <th><code>Location</code><br>name</th>
                    <th><code>Activity</code><br>id</th>
                    <th><code>Activity</code><br>name</th>
                    <th><code>Activity</code><br>nicknames</th>
                </tr>
                <tr>
                    <td rowspan="7">Mount Elbert</td>
                    <td>2</td>
                    <td>Hiking</td>
                    <td></td>
                </tr>
                <tr>
                    <td>3</td>
                    <td>Climbing</td>
                    <td></td>
                </tr>
                <tr>
                    <td>4</td>
                    <td>Mountaineering</td>
                    <td></td>
                </tr>
                <tr>
                    <td>5</td>
                    <td>Trail Running</td>
                    <td></td>
                </tr>
                <tr>
                    <td>6</td>
                    <td>Camping</td>
                    <td></td>
                </tr>
                <tr>
                    <td>7</td>
                    <td>Backpacking</td>
                    <td></td>
                </tr>
                <tr>
                    <td>8</td>
                    <td>Touring</td>
                    <td>Skiing/Snowboarding (Backcountry), Skiing, Off Piste</td>
                </tr>
            </table>
        </td>
    </tr>
</table>
