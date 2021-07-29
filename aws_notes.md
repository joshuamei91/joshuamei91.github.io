---
layout: page
title: AWS Notes
permalink: /aws-cheatcheet/
---

## S3
- Check if bucket exists `aws s3api head-bucket --bucket mybucket`
- Create bucket: `aws s3 mb s3://mybucket`
- [Remove all files from bucket](https://docs.aws.amazon.com/cli/latest/reference/s3/rm.html): `aws s3 rm s3://mybucket --recursive`
- Delete bucket: `aws s3api delete-bucket --bucket mybucket`
- List user owned buckets: 
  - `aws s3api list-buckets`
  - `aws s3 ls`
- List objects in bucket:
  - `aws s3api list-objects-v2 --bucket mybucket --prefix sub/path/`
  - `aws s3 ls s3://mybucket/sub/path`
  - `aws s3 ls s3://mybucket --human-readable --summarize`
- [Get object](https://docs.aws.amazon.com/cli/latest/reference/s3api/get-object.html): `aws s3api get-object --bucket mybucket --key myobject`

