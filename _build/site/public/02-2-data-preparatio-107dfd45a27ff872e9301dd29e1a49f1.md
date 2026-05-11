---
title: Preparing Dataset
---
After downloading the OpenAlex snapshot, we must transform the data into a format that our database software, DuckDB, can use.

Before proceeding, ensure that the snapshot is in the correct directory:

`/network/rit/lab/info-eco/openalex-snapshot/`

Optionally, path values can be modified in the following scripts if locations change.

### Preparing Data

A script to initiate all of the following steps is located at:

`/network/rit/lab/info-eco/scripts/openalex-pipeline/parquet_converter.sh`

The script will take some time, so consider using the nohup command to prevent process hangups from exiting your shell or tmux/screen to preserve your shell.

[miniconda]:/miniconda
