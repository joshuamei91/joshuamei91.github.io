---
layout: page
title: AWS Notes
permalink: /aws-cheatcheet/
---

## S3
- Check if bucket exists `aws s3api head-bucket --bucket mybucket`
- Create bucket: 
  - `aws s3 mb s3://mybucket`
  - `aws s3api create-bucket --bucket mybucket`
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
- Add CA to S3 in Node.js
  ``` node
  s3 = new AWS.s3({
    httpOptions: {
      agent: new https.Agent({
        ca: fs.readFileSync('/path/to/ca.crt')
      })
    }
  })
  ```

### Troubleshooting

#### Invalid Location Constraint when creating bucket using AWS SDK

By default, the bucket will be created in us-east-1. If you are using a custom object store, the Location Constraint might not be us-east-1.
Resolution:
``` bash
aws s3api create-bucket --bucket mybucket # use the cli to create bucket
aws s3api get-bucket-location --bucket mybucket # to check the LocationConstraint eg. "xyz"
```
In the AWS SDK:
``` node
s3.createBucket({
  Bucket: mybucket,
  CreateBucketConfiguration: {
    LocationConstraint: "xyz"
  }
})
```

