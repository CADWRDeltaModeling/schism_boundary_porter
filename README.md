# SCHISM boundary porter
Script to port various flow data formats (e.g., from CalSim, csv, etc.) into SCHISM time history (.th) files

## Directory
(DIR) **data**: directory for substitution data in csv and SCHISM .th files  
(DIR) **output**: script outputs (flux files)

**config.yaml**: configuration parameters, filenames, meta  
**source_map.csv**: substitution instructions for SCHISM variables filenames and calculations (if applicable)
multiple source maps are included as templates  
**port_boundary.py**: main script  