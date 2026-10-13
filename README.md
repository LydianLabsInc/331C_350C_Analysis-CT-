# CT 2W Resistance Increase: Rate Fits (331C / 350C)

Jupyter notebook (`ct_2w_resistance_fits.ipynb`) that loads CT run exports from Nominal, filters
the `Catalyst 2W Resistance` signal to steady operation (target temperature band, pressure > 19 bar,
no N2), puts it on a time-on-stream axis, and fits several resistance-vs-time forms (linear,
exponential, quadratic, power law, linear + power law, geometric) with moving-block bootstrap 95%
confidence intervals.

Runs covered: CT-357P-331C-V4-TS2-R1 (950 °C) and CT-385P-350C-D2-TS1-R1 (1050 °C).

## Get the data

Data files are not stored in this repo. Download raw data files from Nominal
(CT-357P-331C-V4-TS2-R1 and CT-385P-350C-D2-TS1 workbooks from the CT run template). Export
the "Standard Plots" tab to a csv. This will result in a large file. If a lighter file is
desired, export only the Catalyst 2W resistance, Catalyst Outlet Temp, H2, N2, CO2, and
Pressure traces.

Put both CSVs in one folder anywhere on your computer.

## Set up

    pip install -r requirements.txt

## Run

1. Tell the notebook where your CSVs are, in one of three ways:
   - put them in this folder (they're git-ignored, so they won't be committed),
   - set the `CT_DATA_DIR` environment variable to their folder before starting Jupyter/VS Code
     (Windows: `setx CT_DATA_DIR "C:\path\to\exports"`, then restart VS Code), or
   - edit `DATA_DIR` in the notebook's Configuration cell (avoid committing your personal path).

   If your exported file names differ, update `FILES` in the same cell.
2. Run all cells. The fitting section takes several minutes (bootstrap refits).

Figures and `model_parameters.csv` are written to `outputs/` (change with `OUTPUT_DIR` or
`CT_OUTPUT_DIR`).

## Contributing

- Clear all notebook outputs before committing (VS Code: **Clear All Outputs**, then save). This
  keeps data out of the repo and keeps changes readable.
- Notebooks don't merge well. Coordinate who is editing, or work on a branch.

## Caveat

Neither run has a usable 4W signal, so all fits use the 2W resistance, which mixes bulk
material change with contact degradation. The fitted rates are descriptive comparisons,
not kinetic parameters.
