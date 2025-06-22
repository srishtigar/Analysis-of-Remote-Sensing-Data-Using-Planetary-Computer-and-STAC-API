# 🛰️ Remote Sensing Data Analysis with Microsoft Planetary Computer

This project demonstrates how to search, access, and analyze satellite imagery from the Microsoft Planetary Computer using the STAC API and Python tools. It includes NDVI calculation, surface temperature mapping, and color infrared visualization for the Delhi NCR region.

---

## Features
- Query and filter Landsat imagery using STAC API (cloud cover, platform, date)
- Download and process multi-band satellite data with `odc.stac`
- Compute NDVI and surface temperature maps
- Visualize natural color, NDVI, and color infrared composites with Matplotlib
- Summarize and inspect Landsat asset metadata and statistics

---

---

## Getting Started

### Prerequisites

- Python 3.8+
- `pystac-client`
- `planetary-computer`
- `odc-stac`
- `matplotlib`
- `xarray`

### Install dependencies:

pip install pystac-client planetary-computer odc-stac matplotlib xarray


---

## Usage

1. Launch Jupyter and open `landsat_stac_analysis.ipynb`.
2. - Connect to the Microsoft Planetary Computer STAC API
   - Search for recent, low-cloud Landsat images over Delhi NCR
   - Download and process bands of interest
   - Calculate NDVI and surface temperature
   - Visualize results with Matplotlib

---


## Search and select imagery:

import pystac_client, planetary_computer
catalog = pystac_client.Client.open(
"https://planetarycomputer.microsoft.com/api/stac/v1",
modifier=planetary_computer.sign_inplace,
)
bbox = [76.8382, 28.4043, 77.3346, 28.8832]
search = catalog.search(
collections=["landsat-c2-l2"],
bbox=bbox,
datetime="2024-01-01/2024-06-30",
query={"eo:cloud_cover": {"lt": 10}},
)
items = search.item_collection()


**NDVI calculation and visualization:**

import odc.stac, matplotlib.pyplot as plt
bands = ["nir08", "red", "green", "blue", "lwir11"]
data = odc.stac.stac_load([selected_item], bands=bands, bbox=bbox).isel(time=0)
ndvi = (data["nir08"].astype(float) - data["red"].astype(float)) / (data["nir08"] + data["red"])
ndvi.plot.imshow(cmap="viridis")
plt.title("NDVI, Delhi")
plt.show()


---

##  📊 Example Outputs

- **Natural color composite** for Delhi NCR
- **NDVI map** for vegetation analysis
- **Surface temperature map** (in °C) from thermal bands
- **Asset metadata** and band statistics

---




