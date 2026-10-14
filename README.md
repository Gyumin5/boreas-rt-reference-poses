# Reference poses for localization evaluation on Boreas Road Trip

This repository holds the reference poses used to score localization error in our
paper. One file per evaluated sequence and LiDAR, 28 files in all, covering the
nine routes of the Boreas Road Trip dataset.

The navigation solution shipped with the dataset is not registered across sessions:
a map built from one session and a query from another do not share a frame, so an
error measured against it carries that offset. For each route the sessions recorded
on it are therefore jointly optimised into one locally consistent solution, and the
poses released here are that solution sampled at the evaluated scans. Every method
compared in the paper is scored against these same poses.

## File format

Whitespace-separated text, one row per evaluated scan:

| column | meaning |
|---|---|
| 1 | timestamp in nanoseconds, equal to the stem of the scan file it belongs to |
| 2 | easting in metres, UTM zone 17N |
| 3 | northing in metres, UTM zone 17N |
| 4 | height in metres, local vertical datum (not orthometric altitude) |
| 5 | roll in degrees |
| 6 | pitch in degrees |
| 7 | yaw in degrees |
| 8 | constant 1 |

Conventions:

- The pose is that of the vehicle's rear axle, with body axes x forward, y left, z up.
- Yaw is the heading measured from UTM grid north, wrapped to [-180, 180). Compared
  against the course over ground of the released track itself, the two agree to a
  median of 0.17 degrees and a 95th percentile of 1.06 degrees.
- The three angles are extrinsic x-y-z Euler angles in degrees, the convention of
  `scipy.spatial.transform.Rotation.as_euler("xyz", degrees=True)`.
- A row exists only for the scans that were evaluated, so a file has fewer rows than
  the sequence has scans. Match a scan to its pose by the timestamp in column 1,
  which is the scan file's own stem; do not interpolate between rows.

## Contents

| Route | Sequence | LiDAR | Rows |
|---|---|---|---|
| Farm | boreas-2025-07-18-14-55 | velodyne | 7,055 |
| Farm | boreas-2025-08-13-10-36 | velodyne | 7,352 |
| Forest | boreas-2025-07-18-11-00 | velodyne | 5,290 |
| Forest | boreas-2025-07-18-11-53 | velodyne | 5,314 |
| Freeway | boreas-2025-07-18-16-24 | velodyne | 24,203 |
| Freeway | boreas-2025-08-13-11-52 | velodyne | 24,023 |
| Industrial | boreas-2024-12-23-16-27 | aeva | 4,114 |
| Industrial | boreas-2024-12-23-16-27 | velodyne | 4,035 |
| Industrial | boreas-2024-12-23-17-18 | aeva | 4,152 |
| Industrial | boreas-2024-12-23-17-18 | velodyne | 4,069 |
| Regional | boreas-2024-12-03-13-13 | aeva | 5,730 |
| Regional | boreas-2024-12-03-13-13 | velodyne | 5,597 |
| Regional | boreas-2024-12-10-12-07 | aeva | 5,564 |
| Regional | boreas-2024-12-10-12-07 | velodyne | 5,435 |
| Skyway | boreas-2024-12-04-12-08 | aeva | 4,843 |
| Skyway | boreas-2024-12-04-12-08 | velodyne | 4,680 |
| Skyway | boreas-2024-12-04-12-19 | aeva | 4,957 |
| Skyway | boreas-2024-12-04-12-19 | velodyne | 4,789 |
| Suburbs | boreas-2024-12-03-12-54 | aeva | 5,853 |
| Suburbs | boreas-2024-12-03-12-54 | velodyne | 5,760 |
| Suburbs | boreas-2024-12-05-14-25 | aeva | 5,778 |
| Suburbs | boreas-2024-12-05-14-25 | velodyne | 5,700 |
| Tunnel | boreas-2024-12-04-14-28 | aeva | 1,212 |
| Tunnel | boreas-2024-12-04-14-28 | velodyne | 1,200 |
| Tunnel | boreas-2024-12-04-15-19 | aeva | 1,176 |
| Tunnel | boreas-2024-12-04-15-19 | velodyne | 1,154 |
| Urban | boreas-2025-08-06-06-33 | velodyne | 5,319 |
| Urban | boreas-2025-08-06-08-35 | velodyne | 6,387 |

170,741 poses in total.

File names follow `<route>-<sequence>_<lidar>.txt`, with the route in lower case.

## Source data and licence

The poses are derived from the Boreas Road Trip dataset, distributed at
`s3://boreas` and listed in the AWS Registry of Open Data under the
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/legalcode) licence.

- Dataset: https://www.boreas.utias.utoronto.ca
- Registry entry: https://registry.opendata.aws/boreas/

Please cite the dataset:

```bibtex
@article{lisus2026boreasrt,
  author  = {Lisus, Daniil and Papais, Katya M. and Le Gentil, Cedric and
             Preston-Krebs, Elliot and Lambert, Andrew and Leung, Keith Y. K. and
             Barfoot, Timothy D.},
  title   = {{Boreas Road Trip: A Multi-Sensor Autonomous Driving Dataset on Challenging Roads}},
  journal = {arXiv preprint arXiv:2602.16870},
  year    = {2026}
}
```

Changes made to the source data: the poses here are not the navigation solution
released with the dataset. They were re-derived from it, expressed in the rear-axle
frame and in UTM zone 17N, and sampled at the evaluated scans.

This derived material is released under the same
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/legalcode) licence.
