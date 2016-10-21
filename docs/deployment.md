---
layout: default
title: Deployment
---

## Deployment

`thumbsup` is a fully static generator.
The output is a website that can be browsed locally in your favourite browser, or hosted on any webserver.
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

### Deployment

The simplest is to deploy the whole folder to an S3 bucket on AWS using the [AWS CLI](http://aws.amazon.com/cli/).

```bash
aws s3 sync ./generated/website s3://my.website.bucket --delete
```

You can also use [s3cmd](http://s3tools.org/) which offer a few more options.

```bash
s3cmd sync --config=<credentials> --delete-removed --exclude-from <exclude-file> ./generated/website/ s3://my.website.bucket/
```


### Password protection

Amazon S3 buckets do not offer any type of authentication. If you want to protect your galleries, you can

- deploy the galleries to UUID-based locations, like Dropbox shared galleries
- use [CloudFront with signed cookies](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/PrivateContent.html) in front of S3
- deploy to another web server that offers password protection, such as Varnish/Apache/Nginx with `HTTP Basic Auth`
