---
title: Preparing Dataset
---
After downloading the OpenAlex snapshot, we must transform the data into a format that our database software, DuckDB, can use.

Before proceeding, ensure that the snapshot is in the correct directory:

`/network/rit/lab/info-eco/openalex-snapshot/`

Optionally, path values can be modified in the following scripts if locations change.

### Preparing Data

A script to initiate all of the following steps is located at:

`/network/rit/lab/info-eco/scripts/openalex-pipeline/duckdb_pipeline.sh`

The script will take some time, so consider using the nohup command to prevent process hangups from exiting your shell or tmux/screen to preserve your shell.

### Preparation Steps

The OpenAlex dataset is downloaded in batches of gzipped json files. Transforming this data involves:

Unzipping data recursively:
```gunzip -r /network/rit/lab/info-eco/openalex-snapshot```

- Combining batches into single files for each data type:
	- `/network/rit/lab/info-eco/scripts/openalex-pipeline/combine.sh`
- Converting json files into parquet:
	- `/network/rit/lab/info-eco/miniconda/envs/env_duckdb/bin/python /network/rit/lab/info/scripts/openalex-pipeline/parquet_converter.py`
