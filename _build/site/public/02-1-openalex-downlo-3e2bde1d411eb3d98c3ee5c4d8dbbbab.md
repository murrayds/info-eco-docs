---
title: Downloading OpenAlex
---

### Download
Download is performed using the AWS CLI with the following command:

Correct later with proper AWS CLI path.
```
nohup /path/to/aws s3 sync "s3://openalex" "/network/rit/lab/info-eco/openalex-snapshot" --no-sign-request &
```

Data is downloaded as a set of gzip-compressed json files.  Conversion from these files to the parquet file format is handled with a script.

### Conversion
Link to DuckDB/conversion whenever new conversion script is made, requires conda package.
[Dataset Conversion]

[Dataset Conversion]:/03-02-dataset-conversion.md
