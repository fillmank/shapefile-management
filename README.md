# Shapefile Management

This repository contains a Jupyter notebook workflow for processing OpenStreetMap shapefiles for:

- **Buildings**
- **Major roads**
- **State/county reference boundaries**

The notebook reads shapefiles from organized data folders, clips them to a state boundary, joins county information, dissolves features by county, and exports the results.

## Repository Structure

```text
data/
├── buildings/
│   ├── building_file_1.shp
│   ├── building_file_1.shx
│   ├── building_file_1.dbf
│   ├── building_file_1.prj
│   └── ...
├── roads/
│   ├── road_file_1.shp
│   ├── road_file_1.shx
│   ├── road_file_1.dbf
│   ├── road_file_1.prj
│   └── ...
├── reference/
│   ├── your_state_counties.shp
│   ├── your_state_counties.shx
│   ├── your_state_counties.dbf
│   ├── your_state_counties.prj
│   └── ...
└── output/
```

## What the Notebook Does

The notebook:

1. Loads all building shapefiles from `data/buildings/`
2. Loads all road shapefiles from `data/roads/`
3. Reads a county/state boundary shapefile from `data/reference/`
4. Filters the reference layer to your target state
5. Clips buildings and roads to the state boundary
6. Spatially joins features to county boundaries
7. Dissolves features by county
8. Exports results into `data/output/`

## Getting Started

### 1. Install Dependencies

You will need Python 3 and the following packages:

- `geopandas`
- `pandas`
- `pathlib` is part of the Python standard library

You can install the required packages with:

```bash
pip install geopandas pandas
```

If you are using Conda, you can also install GeoPandas with:

```bash
conda install geopandas pandas
```

### 2. Add Your Data

Place your files in the following folders:

- `data/buildings/` for OpenStreetMap building shapefiles
- `data/roads/` for OpenStreetMap major road shapefiles
- `data/reference/` for the county/state boundary shapefile

Important: shapefiles are made up of multiple files. Make sure each dataset includes all required components:

- `.shp`
- `.shx`
- `.dbf`
- `.prj`

### 3. Update the Notebook Variables

Open `shpfile_workflow_bldg_py.ipynb` and update these values as needed:

- `Your State Name`
- `STATE_NAME`
- `COUNTY_NAME`

These field names may vary depending on your reference dataset. Make sure they match the column names in your shapefile.

### 4. Run the Notebook

Run the notebook cells in order. The processed outputs will be written to:

```text
data/output/
```

## Output Files

The notebook generates:

- `Buildings_By_County.shp`
- `Roads_By_County.shp`

These files contain the dissolved building and road geometries grouped by county.

## Common Issues

### No files are being loaded
Make sure your shapefiles are in the correct folder and that the filename pattern matches the notebook.

### Field name errors
If the notebook errors on `STATE_NAME` or `COUNTY_NAME`, inspect your shapefile’s attribute table and update the field names accordingly.

### CRS mismatch
If the geometries do not overlay correctly, ensure all layers are using the same coordinate reference system (CRS). You may need to reproject one or more layers before clipping or joining.

Example:

```python
state_counties = state_counties.to_crs(merged_buildings.crs)
```

## Customization

You can adjust the workflow to:

- use different shapefile names
- process additional feature types
- export to GeoPackage instead of shapefile
- apply different county or state boundaries

## License

Add your preferred license here.

## Contact

Add your contact information or project notes here.
