# Geometry

## Description

VTL 2.0 does not contain geographic types, and therefore no such operator.

## Draft

### 09/19/23 - First proposal (NL)

#### Prerequisites

VTL geometric serializations have to be expressed with **shared standards**.

Proposal:

- handle [**`wkt`**](https://www.ogc.org/standard/wkt-crs/) and [**`geojson`**](https://geojson.org/) as source and target.
- VTL internal representation of geometric objects will be in the `wkt` format (defined by [OGC](https://www.ogc.org/)).

#### Introduce VTL geometric types

- define **`point`** basic scalar type
- define **`polygon`** basic scalar type

#### Geometric type "constructors"

At this point, VTL does not contains constructors (ie new Object(...)).
User are able to instanciate directly a string (`s := "string"`) but not a Date. To do so, user needs to invoke `calc` operator (`d := cast("2023-09-19", date, "YYYY-mm-dd")`).

To make the `calc` signature consistent, we can consider these new possibilities:

- Cast `point` in `string`: `s := cast(myPoint, string, mask)` where mask is the string output format (can be `wkt` or `geojson`)
- Cast `string` in `point`: `s := cast("POINT(10 10)", point, mask)` where mask is the string input format (can be `wkt` or `geojson`, `wkt` in this example)
- Cast `polygon` in `string`: `s := cast(myPolygon, string, mask)` where mask is the string output format (can be `wkt` or `geojson`)
- Cast `string` in `polygon`: `s := cast("POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))", polygon, mask)` where mask is the string input format (can be `wkt` or `geojson`, `wkt` in this example)

#### Define geometric operators

Business usecases needed to define relevant operators.

- Example: point in polygon?

`nuts3`:

|    area    |                    contour                    |
| :--------: | :-------------------------------------------: |
|  integer   |                    polygon                    |
| identifier |                    measure                    |
|     1      | POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10)) |
|     2      |           POLYGON ((0 0, 0 1, 1 0))           |

`cities`:

|     id     |    x    |    y    |
| :--------: | :-----: | :-----: |
|   string   | string  | string  |
| identifier | measure | measure |
|    "A"     |  "0.2"  |  "0.2"  |
|    "B"     |  "20"   |  "20"   |
|    "C"     |  "100"  | "-100"  |
|    "D"     |  "21"   |  "21"   |

`VTL script`:

```
cities := cities[calc xyStr := "POINT(" || x || " " || y || ")"]
                [drop x, y]
                [calc xy := cast(xyStr, point, "wkt")]
                [drop xyStr];
```

`cities`:

|     id     |       xy        |
| :--------: | :-------------: |
|   string   |      point      |
| identifier |     measure     |
|    "A"     | POINT(0.2 0.2)  |
|    "B"     |  POINT(20 20)   |
|    "C"     | POINT(100 -100) |
|    "D"     |  POINT(21 21)   |

`VTL script`:

```
// how to obtain result as a city table where cities are contained in areas?
// define dedicated operator?
result := geo_includes(cities, nuts3 using xy, contour)
// or simply cross_join using the filter clause
result := cross_join(cities, nuts3 filter geo_includes(xy, contour));
```

`result`:

|     id     |       xy       |  area   |                    contour                    |
| :--------: | :------------: | :-----: | :-------------------------------------------: |
|   string   |     point      | integer |                    polygon                    |
| identifier |    measure     | measure |                    measure                    |
|    "A"     | POINT(0.2 0.2) |    2    |           POLYGON ((0 0, 0 1, 1 0))           |
|    "B"     |  POINT(20 20)  |    1    | POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10)) |
|    "D"     |  POINT(21 21)  |    1    | POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10)) |

### 09/22/23 - Meeting notes (NL - VP - JS - FV)
