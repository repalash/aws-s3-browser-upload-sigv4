<!--
title: 'Browser-Based Upload using HTTP POST (Using AWS Signature Version 4)'
description: 'Upload files using simple HTML Form POST request to S3 with signature v4 signed post policy.'
layout: Doc
language: nodeJS
authorLink: 'https://github.com/palashbansal96'
authorName: palashbansal96
-->

# Browser-Based Upload using HTTP POST (Using AWS Signature Version 4)

An example code to show an example of using an HTTP POST request to upload content directly to Amazon S3 with signature v4 signed post policy.

`generate-form.js` is node.js based generator script to make an HTML form similar to AWS docs example for [Browser based uploads to S3](https://docs.aws.amazon.com/AmazonS3/latest/API/sigv4-post-example.html)

## Use-cases

- Generate HTML forms to upload files to S3 with a fixed policy, without the need for a backend.
- Demonstrate POST Policy Signature Version 4 (AWS4-HMAC-SHA256) signing process from scratch in js.
- DO NOT use this in production with an open setting with a fixed policy and infinite expiry. Use aws-sdk to generate a presigned URL for upload.

## Setup

- Create a new S3 bucket, with public access enabled. (Block all public access should be unchecked during bucket creation).
- Edit `generate-form.js` and fill in your `aws_access_key_id`,
  `aws_secret_access_key`, `bucket_name` and `region`.
- Run `yarn/npm install` to install crypto-js dependency for `generate-form.js`.
- Add any meta-data for the file to `index.template.html`
- Generate the HTML form with signature and policy with `node generate-form.js`


```bash
yarn install
node generate-form.js
```

## Usage

Open the generated `index.html` in your browser, or run:

```bash
xdg-open frontend/index.html
```

Select a PNG image smaller than 1Mb, and click "Upload File to S3".

You should get an XML response similar to:

```xml
<PostResponse>
  <Location>https://bucket-name.s3.amazonaws.com/uploads%2Fimage.png</Location>
  <Bucket>serverless-fetch-file-and-store-in-s3</Bucket>
  <Key>uploads/image.png</Key>
  <ETag>"08c03c6a24e5058b9f3556981a23b1d7"</ETag>
</PostResponse>
```

The file can now be seen in the AWS console with all the object meta-data.
You can also specify a `success_action_redirect` form field in HTML to redirect on success.