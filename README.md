This repository holds two exploratory exercises on road-network data quality in Paradise, California. Exercise 2 is described at the bottom of this page.

# Missing roads and evacuation exits: a small test in Paradise, California

A small Python exercise (OSMnx, NetworkX) testing how missing street segments change which exits look busiest and how many intersections can still reach an exit. Intersections inside the town boundary stand in for homes. See the notebook for the method, results, and limits.

This is a simplified exercise, not a replication of published models.


---

## Exercise 2: Facility location under incomplete road-network data

Exploratory exercise. Not a validated evacuation model.

### Question
If a planner works from a road network with missing segments, how much worse are the
chosen emergency-station locations when judged on the full network?

### Method
- Road network from OpenStreetMap (OSMnx), treated as two-way, largest connected component.
- 150 random intersections as demand points; 60 random intersections as candidate sites.
- p-median model (p = 3), solved with SciPy (HiGHS) on the full network = plan A.
- 5, 10 and 20% of road segments removed: random (20 repeats) and busiest (sampled betweenness).
- Plan B chosen on the incomplete network, then evaluated on the full network.
- Metrics: stations changed, extra distance vs plan A (%), demand points with no route.
- Repeated on three further random samples of demand points and sites (10 random repeats each).

### Main results
- Across four random samples, planning on a network with road segments removed at random cost on
  average 9-14% extra distance at 5% removal, 15-27% at 10% and 18-29% at 20%, judged on the full network.
- Busiest-segment removal was a single scenario per level and was not consistently worse than random.

### Limitations
One town; intersections stand in for homes and sites; equal weights; two-way roads;
betweenness instead of observed traffic; sampled points; busiest-segment removal is one
scenario per level; not a validated model and not a replication of published models.

### Files
Paradise_pmedian_incomplete_network.ipynb, pmedian_results.csv, pmedian_regret.png,
pmedian_results_other_seeds.csv
