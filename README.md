# Geospatial Analysis of the 2022 Flood Event in Kogi State, Nigeria

This project is a humanitarian-focused case study demonstrating a complete geospatial workflow to assess the impact of the severe 2022 floods in Kogi State, Nigeria. The analysis identifies the flood extent, estimates the affected population, and locates impacted health facilities to support humanitarian decision-making.

This portfolio piece was developed to showcase the importance of geospatial techniques in addressing environmental issues and providing informed decision-making support. 

## Key Findings

*   **Estimated Population Affected:** 104,880 people
*   **Identified Health Facilities in Flooded Zones:** 22
*   **Total Flooded Area:** 

_  **Interactive Web Map:** An interactive version of the map can be viewed by downloading `Nigeria_Flood_Analysis_Final.html` and opening it in a browser.

## Technical Workflow & Technologies Used

The project follows a systematic workflow from raw data processing to final analysis:

1.  **Data Sourcing & Pre-processing:**
    *   Cloud-free Sentinel-2 satellite mosaics were created for pre-flood (Jan-Feb 2022) and during-flood (Oct 2022) periods using **Google Earth Engine (GEE)**.
    *   Administrative boundaries (FAO), health facility locations (Shapefile from HDX, uploaded as a GEE Asset), and high-resolution population data (JRC GHSL) were integrated.

2.  **Analysis in Google Earth Engine:**
    *   The **Modified Normalized Difference Water Index (MNDWI)** was used to accurately delineate surface water.
    *   Change detection between the two periods isolated the flood-only areas (`flood_extent`).
    *   The high-resolution GHSL population layer was overlaid with the flood extent to calculate the `affected_pop_count`.
    *   A spatial join between the flood polygons and the health facilities asset identified `affected_health_facilities`.

3.  **Data Export & Management:**
    *   The complex flood polygons were simplified using `f.simplify()` to manage data size for export.
    *   Final vector layers (`flood_extent`, `affected_health_facilities`) were exported from GEE via Google Drive as GeoJSON files.
    *   The Python script uses **GeoPandas** to load these files and **SQLAlchemy/psycopg2** to load the data into a **PostGIS / PostgreSQL** database for robust storage and querying.

4.  **Key Technologies:**
    *   **Cloud GIS Platform:** Google Earth Engine
    *   **Core Libraries:** Python, `geemap`, `geopandas`, `pandas`, `sqlalchemy`
    *   **Database:** PostgreSQL with PostGIS extension
    *   **Desktop GIS:** QGIS (for final cartography)
    *   **Version Control:** Git & GitHub

## How to Run This Project

1.  Clone this repository.
2.  Set up a local PostGIS database (e.g., via Docker).
3.  Ensure your Conda environment has the necessary packages (a `conda create` command is provided in the notebook for reproducibility).
4.  Run the `Nigeria Flood Analysis.ipynb` notebook from top to bottom. The notebook handles GEE authentication, analysis, and loading data into the local PostGIS instance.
