---
title: Downloading OpenAlex
---

### Installing AWS Cli
Install the AWS Cli tool to your ~/local/bin/ by navigating to:
`/network/rit/lab/info-eco/installer/aws/`
Read README.md, specifically the section titled: Installing without sudo

Then run the install script with the appropriate commands.

### Download
Download is performed using the AWS CLI with the following below:

Replace /path/to/aws with your ~/.local aws path! Example: `~/.local/bin/aws`
```
nohup /path/to/aws s3 sync "s3://openalex" "/network/rit/lab/info-eco/openalex-snapshot" --no-sign-request &
```

Data is downloaded as a set of gzip-compressed json files.  Conversion from these files to the parquet file format is handled with a script.  Refer to [dataset conversion].

[dataset conversion]: /parquet-conversion
