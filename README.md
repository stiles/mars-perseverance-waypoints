# Percy waypoints

This repository contains code that automatically tracks the location of the Mars Perserverance rover, known as Percy, using Github Actions and [feeds](https://mars.nasa.gov/maps/location/?mission=M20) from NASA. The scripts run hourly.

## Inputs

The actions collect data from a two raw sources that feed NASA's rover [mapping application](https://mars.nasa.gov/maps/location/?mission=M20): 

- **Latest location** | [JSON](https://mars.nasa.gov/mmgis-maps/M20/Layers/json/M20_waypoints_current.json)
    - *Collected hourly*

- **Latest mission update** | [JSON](https://mars.nasa.gov/maps/location/api/configure/get?mission=M20)
    - *Collected hourly*

### Processing

The path and waypoints files are collected hourly and stored in a ["raw" directory](/data/raw/), with files stamped by the calendar date. Each daily file is the last location or mission update collected and committed during that day, if the location changes. 

For example, the waypoints:

```
waypoints_current_2024-04-04.json
waypoints_current_2024-03-31.json
waypoints_current_2024-04-01.json
```

And the mission files:

```
mission_2021-03-15.json
mission_2021-03-16.json
mission_2021-03-17.json
```

Those files are then collected, read, concatenated and processed in a [Jupyter notebook](/00-combine-daily-waypoints.ipynb) that outputs combined points and path files in GeoJSON format. 

### Outputs

- **Rover waypoints collection** | [GeoJSON points](data/processed/rover_points_full.geojson)
    - *March 15, 2021 - present*
- **Rover full path** | [GeoJSON linestring](data/processed/rover_path_full.geojson)
    - *March 15, 2021 - present*


Happy roving! 

---

**Questions? Thoughts?** 
Please [email me](mailto:mattstiles@gmail.com). 