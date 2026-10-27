# Changes from upstream

This copy starts from the file tree of https://github.com/GEOS-ESM/MERRA-2_FLUID at commit `d21e7237d1a81815c6644552d0c236bad15158f4` (tag v1.0.0, 2025-02-04), without its git history. The `.github/` folder (CODEOWNERS and CI workflows for the upstream repository) is left out. The code is by NASA GMAO under the license in `LICENSE`.

## 2026-10-27: README names the run order of the monthly extremes indices

The README did not say which scripts build the monthly M2SMNXEDI file or in what order. It now lists the five scripts in `m2stats/NCAindices/monthly/`, their arguments (`yyyy mm climoperiod`, or `yyyy mm` for the shell step) and the order they must run in: `computeRindices.py`, `computeTndays.py`, `compute_heatwave_indices.py`, `get5dayprecip.bash`, `computeRx5day.py`. Steps 2 to 5 add to the file step 1 creates, and step 5 reads step 4's output. No code changed, so no results change.

Who asked for it: the registration wizard (it found no start-up command and asked which command runs the algorithm). The wording and order are ours.

## 2026-10-27: the monthly scripts exit with status 0 on success

`computeRindices.py`, `computeTndays.py` and `computeRx5day.py` ended with `sys.exit(1)` after writing their results, so every successful run reported failure to the shell, a batch system or a job runner. They now end with `sys.exit(0)`. The error exit in `computeRx5day.py` (line 63, for a month outside 1 to 12) still exits 1. No results change.

Who asked for it: the registration wizard named `computeRindices.py:236-237` ("for you to judge"). The same line in `computeTndays.py` and `computeRx5day.py` was changed by us, since all three run in the same sequence.
