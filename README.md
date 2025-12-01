# Forest Loss → MIDI (Saxony)

This repo contains a small pipeline of Jupyter notebooks that:

1. Download and preprocess **Global Forest Change** data for Saxony (Germany),
2. Extract and classify spatial clusters of forest loss, and
3. Turn those clusters into **MIDI tracks** – a sonification of deforestation patterns over time.

The workflow focuses on the federal state of **Saxony (Sachsen)** and uses the **Hansen Global Forest Change v1.12 (2000–2024)** dataset. :contentReference[oaicite:0]{index=0}  

---

## Data Source & Attribution

Forest change data:

> **Source:** Hansen/UMD/Google/USGS/NASA :contentReference[oaicite:1]{index=1}  

The underlying dataset is:

> Hansen, M. C., P. V. Potapov, R. Moore, M. Hancher, S. A. Turubanova, A. Tyukavina, D. Thau, S. V. Stehman, S. J. Goetz, T. R. Loveland, A. Kommareddy, A. Egorov, L. Chini, C. O. Justice, and J. R. G. Townshend. 2013. **High-Resolution Global Maps of 21st-Century Forest Cover Change.** *Science* 342 (15 November): 850–853. https://doi.org/10.1126/science.1244693. Data available via the GLAD Global Forest Change app. :contentReference[oaicite:2]{index=2}  

Tiles are downloaded from the official Hansen/UMD Google Cloud bucket. :contentReference[oaicite:3]{index=3}  

Administrative boundaries for Germany/Saxony are pulled from the **GADM 4.1** shapefile (level 1 = states).

---

## Repository Structure

Key pieces:

- `DownloadAndPrepareData.ipynb`  
  Clip Hansen rasters to Saxony, compute yearly statistics, and make overview plots.

- `BuildAndClassifiyClusters.ipynb`  
  Label connected patches (clusters) of forest loss, compute shape metrics, classify them as **points / lines / planes**, and export per-year cluster datasets.

- `MIDIcreation.ipynb`  
  Map cluster properties to musical parameters (pitch, velocity, duration, onset) and export yearly MIDI files.

Typical folders/files created by the notebooks:

- `data/` – Hansen GeoTIFF tiles and other raw data
- `gadm_germany/` – GADM shapefiles for German states
- `hansen_lossyear_saxony.tif`, `hansen_treecover2000_saxony.tif` – clipped rasters
- `saxony_forest_loss_extended.csv` – yearly forest loss metrics for Saxony
- `loss_clusters_all_years.gpkg` / `loss_clusters_all_years.csv` – cluster-level features across all years
- `loss_clusters_summary_by_year.csv` – per-year summary stats
- `*.png` – plots (time series, maps, cluster charts)
- `midi_output_clock/` – exported MIDI files and parameter `.txt` files

---

## Dependencies

All notebooks are standard Python/Jupyter and use:

- Core: `python`, `jupyter`, `numpy`, `pandas`
- Geo stack: `geopandas`, `shapely`, `rasterio`, `rasterio.mask`, `rasterio.warp`
- Image/metrics: `matplotlib`, `scikit-image`
- ML / stats: `scikit-learn`
- I/O / HTTP: `requests`, `zipfile`, `io`, `os`
- MIDI: `pretty_midi`

Install (minimal example, adjust to your environment):

```bash
pip install numpy pandas geopandas shapely rasterio scikit-image scikit-learn matplotlib pretty_midi requests
```
