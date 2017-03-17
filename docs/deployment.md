---
layout: default
title: Deployment
---

## Deployment

`thumbsup` is a fully static generator. The output is fully self-contained, and uses relative links.
This means it be browsed from disk in your favorite browser, or hosted on any simple web server.
There is no application server needed.

### Generated gallery structure

The generated static website has the following structure:

```bash
website
  |
  |   # all albums
  |   # which are just HTML pages
  |__ index.html
  |__ sydney.html
  |__ paris.html
  |
  |   # files to support the website
  |   # e.g. scripts, css...
  |__ public
  |
  |   # your photos and videos
  |   # including resized versions and thumbnails
  |__ media
```

### Deploying to AWS

The simplest way to deploy a `thumbsup` gallery on the internet is to sync
the output folder to Amazon S3 using the [AWS CLI](http://aws.amazon.com/cli/).

```bash
aws s3 sync ./generated/website s3://my.website.bucket --delete
```

You can also use [s3cmd](http://s3tools.org/) which offer a few more options.

```bash
s3cmd sync --config=<credentials> --delete-removed --exclude-from <exclude-file> ./generated/website/ s3://my.website.bucket/
```

Simply enable *website hosting* on S3, and point your user-facing domain to S3 website URL. For example:

```
CNAME mybucket.s3-website-us-east-1.amazonaws.com
```

### Adding password protection

If you want to protect your galleries, you can

- deploy your website behind a web server like `Nginx` or `Apache` and configure basic authentication
- deploy the galleries to UUID-based locations, like Dropbox shared galleries
- deploy to S3 with [CloudFront with signed cookies](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/PrivateContent.html)

#### CloudFront signed cookies

AWS S3 does not support authentication itself. However you can front S3 with the CloudFront CDN,
which supports authentication through cookies. The two main steps are

**Step 1: serve your gallery through CloudFront**

- configure CloudFront, preferably using HTTPS, using an origin of `mybucket.s3.amazonaws.com`
- you can disable website hosting on the bucket, which is not needed anymore
- repoint your user-facing domain to the CloudFront endpoint intead of S3, e.g. [https://00000000.cloudfront.net](#)
- remove public access from the Bucket in the "permissions" section
- grant CloudFront access using the following *Bucket Policy*

```json
{
   "Version":"2012-10-17",
   "Id":"PolicyForCloudFrontPrivateContent",
   "Statement":[
     {
       "Sid":" Grant CloudFront access to all objects",
       "Effect":"Allow",
       "Principal":{
         "AWS": "arn:aws:iam::cloudfront:user/CloudFront Origin Access Identity 0000000000000"
       },
       "Action":"s3:GetObject",
       "Resource":"arn:aws:s3:::website.com/*"
     },
 		{
 			"Sid": "Grant access to list objects, so S3 can return 404 instead of 403",
 			"Effect": "Allow",
 			"Principal": {
 				"AWS": "arn:aws:iam::cloudfront:user/CloudFront Origin Access Identity 0000000000000"
 			},
 			"Action": "s3:ListBucket",
 			"Resource": "arn:aws:s3:::website.com"
 		}
   ]
}
```

At this point you should have a working gallery going through CloudFront, with the added benefit of caching! Serving the gallery from CloudFront is both much faster and less expensive than serving it from S3 (e.g. data transfer costs).

**Step 2: adding authentication**

- setup a new Lambda function using [lambda-cloudfront-cookies](https://github.com/thumbsup/lambda-cloudfront-cookies). Its job is to create authentication cookies when presented with valid credentials
- add a login page to the S3 bucket that contains your galleries, e.g. `s3://website.com/login.html`. You can find a nice-looking template at [thumbsup/html-pages](https://github.com/thumbsup/html-pages)
- setup CloudFront to require auth cookies for all pages
- setup CloudFront to render the login page on `403` errors. This is why the `s3:ListBucket` permission is important, otherwise CloudFront will render the login page for broken links too
- update the login page `<form action="....">` to point to the Lambda API endpoint
