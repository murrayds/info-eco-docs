---
title: OpenAlex
---

# The OpenAlex dataset is a essentially a map of research data, including things like articles, authors, universities, and references.

### Relevant Links
[OpenAlex Documentation] is the documentation hub for the OpenAlex research dataset.

[AWS CLI for Download] is the tool we use for downloading the database.

[Browse Dataset]

[OpenAlex Documentation]: https://developers.openalex.org/
[AWS CLI for Download]: https://developers.openalex.org/download/download-to-machine
[Browse Dataset]: https://openalex.s3.amazonaws.com/browse.html

# Downloading OpenAlex
### Installing AWS Cli
Install the AWS Cli tool to your ~/local/bin/ by navigating to:
`/network/rit/lab/info-eco/installer/aws/`
Read README.md, specifically the section titled: Installing without sudo

Then run the install script with the appropriate commands.

### Download
Download is performed using the AWS CLI tool installed to your ~/.local/bin with the following command:

```
nohup ~/.local/bin/aws s3 sync "s3://openalex" "/network/rit/lab/info-eco/openalex-snapshot" --no-sign-request &
```

Data is downloaded as a set of gzip-compressed json files.  Conversion from these files to the parquet file format is handled with a script.  Refer to [Preparing Dataset].

# Data Preparation

**Important: File paths are hard-coded in scripts. If file locations change, the values must be adjusted.**

After downloading the OpenAlex snapshot, we must transform the data into a format that our database software, DuckDB, can use.

Before proceeding, ensure that the snapshot is in the correct directory:

`/network/rit/lab/info-eco/openalex-snapshot/`

Optionally, path values can be modified in the following scripts if locations change.

### Preparing Data

A script to initiate all of the following steps is located at:

`/network/rit/lab/info-eco/scripts/openalex-pipeline/duckdb_pipeline.sh`

The script will take some time, so consider using the nohup command to prevent process hangups from exiting your shell or tmux/screen to preserve your session.

### Preparation Steps

The OpenAlex dataset is downloaded in batches of gzipped json files. Transforming this data involves:

- Unzipping data recursively:

`gunzip -r /network/rit/lab/info-eco/openalex-snapshot`

- Combining batches into single files for each data type:

`/network/rit/lab/info-eco/scripts/openalex-pipeline/sub/combine.sh`

- Converting json files into parquet:

`/network/rit/lab/info-eco/miniconda/envs/env_duckdb/bin/python /network/rit/lab/info/scripts/openalex-pipeline/sub/parquet_converter.py`

