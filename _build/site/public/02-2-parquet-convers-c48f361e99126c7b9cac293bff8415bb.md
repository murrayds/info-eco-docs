---
title: Parquet Conversion
---
The following is used to convert our compressed snapshot into data readable by DuckDB.  Ensure that the OpenAlex snapshot is downloaded to the correct directory.

```/network/rit/lab/info-eco/openalex-snapshot/```

### Preparing Data

Activate the miniconda environment that contains the DuckDB package, currently:

```conda activate env_duckdb```

If you haven't done your conda setup yet, refer to [miniconda]

Now, run the converter script located in:

```/network/rit/lab/info-eco/scripts/data/parquet_converter.py```

The script will take some time, so consider using the nohup command to prevent hangups from exiting your shell or tmux/screen to preserve your shell.

[miniconda]:/miniconda
