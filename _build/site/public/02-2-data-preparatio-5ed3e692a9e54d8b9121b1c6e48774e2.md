---
title: Preparing Dataset
---
After downloading the OpenAlex snapshot, we must transform the data into a format that our database software, DuckDB, can use.

Before proceeding, ensure that the snapshot is in the correct directory:

`/network/rit/lab/info-eco/openalex-snapshot/`

Optionally, path values can be modified in the following scripts if locations change.

### Preparing Data

Activate the miniconda environment that contains the DuckDB package, currently:

`conda activate env_duckdb`

If you haven't done your conda setup yet, refer to [miniconda]

Now, run the converter script located in:

`/network/rit/lab/info-eco/scripts/data/parquet_converter.py`

The script will take some time, so consider using the nohup command to prevent process hangups from exiting your shell or tmux/screen to preserve your shell.

[miniconda]:/miniconda
