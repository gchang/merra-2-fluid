# Changes from upstream

This copy starts from the file tree of https://github.com/GEOS-ESM/MERRA-2_FLUID at commit `d21e7237d1a81815c6644552d0c236bad15158f4` (tag v1.0.0, 2025-02-04), without its git history. The `.github/` folder (CODEOWNERS and CI workflows for the upstream repository) is left out. The code is by NASA GMAO under the license in `LICENSE`.

## 2026-10-27: README names the run order of the monthly extremes indices

The README did not say which scripts build the monthly M2SMNXEDI file or in what order. It now lists the five scripts in `m2stats/NCAindices/monthly/`, their arguments (`yyyy mm climoperiod`, or `yyyy mm` for the shell step) and the order they must run in: `computeRindices.py`, `computeTndays.py`, `compute_heatwave_indices.py`, `get5dayprecip.bash`, `computeRx5day.py`. Steps 2 to 5 add to the file step 1 creates, and step 5 reads step 4's output. No code changed, so no results change.

Who asked for it: the registration wizard (it found no start-up command and asked which command runs the algorithm). The wording and order are ours.
