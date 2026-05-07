---
title: Downloading OpenAlex
---

### Download
Download is performed using the AWS CLI with the following command:

Correct later with proper AWS CLI path.
```
nohup /path/to/aws s3 sync "s3://openalex" "/network/rit/lab/info-eco/openalex-snapshot" --no-sign-request &
```
