# LTE network design: San Cristóbal and Usme, Bogotá

Coverage dimensioning of an LTE FDD network for the urban area of two localities in southern Bogotá, Colombia. Course project for Cellular Communications at Universidad del Norte. **In progress:** Part 1 (coverage) is complete; capacity dimensioning comes next.

**Interactive map:** [andresjsaco.vercel.app/lte](https://andresjsaco.vercel.app/lte/)

## Results (Part 1: coverage)

| Parameter | Value |
|---|---|
| Operator and band | Claro Colombia, LTE band 2 (PCS 1900 MHz), FDD, 20 MHz |
| Typical station | Type 3: antenna at 30 m, shadow fading margin 8 dB, penetration loss 9 dB, MCS 12 |
| Propagation model | COST-231 Hata |
| Maximum allowable path loss (DL / UL) | 131.96 dB / 128.12 dB |
| Cell radius (DL / UL) | 0.693 km / 0.561 km |
| Effective radius | 0.561 km (uplink limited) |
| Area per three-sector eNB | 0.613 km² |
| Design area | 47.68 km² across 12 urban UPZ |
| Number of eNBs | 78 |
| Inter-site distance | 842 m |
| Area covered at design radius | 97.4% |

## Method

1. **Design area.** Official UPZ (zoning unit) polygons for San Cristóbal and Usme; the 12 urban UPZ form the design area.
2. **Link budget.** Downlink and uplink budgets for band 2 with the parameters of the chosen typical station, giving the maximum allowable path loss in each direction.
3. **Cell radius.** COST-231 Hata solved for distance at each MAPL. The uplink gives the smaller radius, so it sets the effective cell radius.
4. **Site count.** Design area divided by the hexagonal area of a three-sector site.
5. **Site placement.** eNBs placed on a hexagonal grid with an 842 m inter-site distance. The grid offset and rotation were searched to maximise coverage of the actual UPZ boundaries.
6. **Equipment.** Ericsson Baseband 6630, Ericsson Radio 4438 (B2/B66) remote radio units and Andrew (CommScope) NHH-65B-R2B antennas (65°, 17.7 dBi). Each sector transmits 40 W (46 dBm), with 7° electrical tilt and azimuths of 36°, 156° and 276°.

## Repository contents

| Path | Content |
|---|---|
| `data/lte_san_cristobal_usme.kml` | Google Earth file: UPZ boundaries, 78 eNBs with technical sheets, 234 sector footprints and coverage circles |
| `data/enb_sites.csv` | Coordinates, locality, UPZ and sector azimuths for every eNB |
| `data/*.geojson` | The same layers in GeoJSON |
| `docs/index.html` | Interactive Leaflet map |
| `report/LTE_coverage_report_ES.pdf` | Full report (Spanish) |
| `report/latex/` | LaTeX source of the report |

## Next steps

- Part 2: capacity dimensioning, comparing the coverage-limited site count with the capacity-limited one.
- Refine the propagation analysis with terrain data, since both localities are hilly.

Built with Python, LaTeX (TikZ, pgfplots), Google Earth KML and Leaflet.
