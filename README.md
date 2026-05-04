# Forest Cover Analysis: Western Area Peninsula National Park

Analysis of forest cover and forest loss (2001–2023) within the
Western Area Peninsula National Park (WAPNP), Sierra Leone, using the
[Hansen Global Forest Change](https://www.science.org/doi/10.1126/science.1244693)
dataset (GFC v1.11, 2023).

---

## What the code does

The Jupyter notebook (`analysis.ipynb`) performs the following steps:

1. Loads the park boundary from `data/wapnp_boundary.shp`.
2. Extracts the relevant spatial subset of the Hansen treecover2000 and
   lossyear rasters from Google Cloud Storage using windowed rasterio reads
   (no large file downloads required).
3. Calculates the percentage of the park classified as forest (≥ 30 % canopy
   cover) in the year 2000.
4. Computes annual forest loss within the park for each year from 2001 to 2023.
5. Calculates zonal statistics (mean, median, min, max canopy cover) using
   `rasterstats`.
6. Produces a static two-panel figure (forest cover map + annual loss chart)
   saved to `outputs/wapnp_forest_cover_map.png`.
7. Produces an interactive Folium map saved to
   `outputs/wapnp_interactive_map.html`.

---

## Requirements

- [conda](https://conda-forge.org/download/) or
  [Anaconda Navigator](https://www.anaconda.com/download/success)
- [git](https://git-scm.com/downloads)
- Internet access (the notebook downloads Hansen raster subsets on first run)

---

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/CharlotteBond/wapnp-forest-analysis.git
cd wapnp-forest-analysis
```

### 2. Create the conda environment

```bash
conda env create -f environment.yml
conda activate wapnp-forest
```

Or, using Anaconda Navigator: open the **Environments** panel, click
**Import**, and select `environment.yml`.

### 3. Launch JupyterLab

```bash
jupyter lab
```

Open `analysis.ipynb` and run all cells.

---

## Data

| File | Description | Source |
|------|-------------|--------|
| `data/wapnp_boundary.geojson` | Approximate park boundary polygon | Derived from [Protected Planet](https://www.protectedplanet.net/555547936) |
| Hansen treecover2000 | Tree canopy cover (%) for year 2000 | Downloaded automatically by the notebook from Google Cloud Storage |
| Hansen lossyear | Year of first forest loss per pixel (2001–2023) | Downloaded automatically by the notebook from Google Cloud Storage |



---

## Expected outputs

After running `analysis.ipynb` you should see:

- A printed summary table showing forest cover percentage and total loss.
- `outputs/wapnp_forest_cover_map.png` — static two-panel figure.
- `outputs/wapnp_interactive_map.html` — interactive Folium map (open in any
  browser).

---

## Troubleshooting

See `HOWTO_GUIDE.pdf` (Assessment 1) for a full troubleshooting section.
Common issues:

- **SSL / network errors when downloading Hansen data** — try setting the
  environment variable `GDAL_HTTP_UNSAFESSL=YES` before launching JupyterLab.
- **`ModuleNotFoundError`** — ensure you have activated the `wapnp-forest`
  environment before launching JupyterLab.
- **Jupyter opens in the wrong folder** — launch JupyterLab from inside the
  cloned repository directory.

---

## License

[MIT License](LICENSE) — Charlotte Bond, 2026.

---

## References

Hansen, M.C. et al. (2013) High-resolution global maps of 21st-century forest
cover change. *Science*, 342(6160), pp. 850–853.
doi: [10.1126/science.1244693](https://doi.org/10.1126/science.1244693)

Food and Agriculture Organization of the United Nations (FAO) (2020)
*Global Forest Resources Assessment 2020: Main Report*. Rome: FAO.
doi: [10.4060/ca9825en](https://doi.org/10.4060/ca9825en)
