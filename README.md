# MERRA-2_FLUID

This repository contains codes that are used to derive statistics and generate imagery for display under FLUID.

## Running: monthly extremes indices (M2SMNXEDI)

The monthly file `MERRA2.statM_2d_edi_Nx.v2_1.<yyyymm>.nc4` (GES DISC M2SMNXEDI) is built by five steps in `m2stats/NCAindices/monthly/`, run in this order for one month. Each Python step takes `yyyy mm climoperiod` (for example `2025 7 19902020`; climoperiod names the percentile and climatology files, currently `19902020`); the shell step takes `yyyy mm`.

1. `python computeRindices.py yyyy mm climoperiod`: precipitation indices (creates the monthly file).
2. `python computeTndays.py yyyy mm climoperiod`: temperature threshold day counts.
3. `python compute_heatwave_indices.py yyyy mm climoperiod`: heat wave and warm and cold spell indices.
4. `bash get5dayprecip.bash yyyy mm`: daily and running 5-day precipitation totals with lats4d, written to `tmp/` under the folder it is run from. Run it from the folder whose `tmp/` `computeRx5day.py` reads.
5. `python computeRx5day.py yyyy mm climoperiod`: RX5Day and the 5-day heavy precipitation count, from step 4's output.

Steps 2 to 5 add to the file that step 1 creates. The steps read MERRA-2 collections and the percentile and climatology files from the paths written in each script.
