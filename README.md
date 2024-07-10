# SCHISM boundary porter
Script to port various flow data formats (e.g., from CalSim, csv, etc.) into SCHISM time history (.th) files

## Directory
(DIR) **calsim**: place CalSim DSS files in here.
(DIR) **data**: directory for substitution data in csv and SCHISM .th files  
(DIR) **output**: script outputs (flux files)

**config.yaml**: configuration parameters, filenames, meta  
**source_map.csv**: substitution instructions for SCHISM variables filenames and calculations (if applicable)
multiple source maps are included as templates  
**port_boundary.py**: main script  

## Hello `schism_boundary_porter`
Run the boundary porter, as contained in this repo, in three (four) steps.  

0. Install [miniconda](https://docs.anaconda.com/miniconda/)
1. Create environment `conda env create -f environment.yaml`
2. Place a CalSim 3 dss file in the `calsim` directory. This example has been set up to use the dss file from
 the [Draft DCR 2023 Baseline CalSim 3 study](https://data.cnra.ca.gov/dataset/calsim-3-studies-used-in-dcr-2023/resource/0f5be940-6b02-43e4-a8f8-fddd3fd8a794). The DSS filename is DCR2023_DV_9.0.0_Danube_Adj_v1.2.dss.
3. `python port_boundary.py`

## Description of souce_map.csv
`source_map.csv` is the main instruction file for the boundary porter. It instructs the script on what variables to "port", where to find them, and optional parameters (i.e. conversions, smoothing sign)
|Column|Description|
|------|-----------|
|schism_boundary|name of the SCHISM variable|
|boundary_kind|flow,ec,temp|
|source_kind|DSS,CSV,SCHISM,CONSTANT|
|derived|`TRUE` or empty|
|source_file|relative path to the file of `source_kind`|
|var|variable pathname. If `source_kind` is DSS then format is //BPART/CPART//EPART/FPART/|
|sign|-1 or 1, to flip the flow direction|
|convert|CFS_CMS or EC_PSU|
|rhistinterp|spline tension for rational histospline interpolation from [vtools/vtools/functions/interpolate.py](https://github.com/CADWRDeltaModeling/vtools/blob/8366ab7c48359ed3d871aa48007a0ba8fbc7e5cc/vtools/functions/interpolate.py#L245)
|formula|if `convert` is `TRUE` then add formula here. `See source_map_example.csv` for example format|
|note|optional note|