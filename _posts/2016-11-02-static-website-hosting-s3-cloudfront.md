---
title: Static Website Hosting with S3 and CloudFront
date: 2015-11-02 12:00:00 Z
description: Host your static website on AWS S3 and CloudFront
published: false
header-img: 
layout: post
---

After many hours of debugging and a few sessions with AWS support engineers, I'm happy to share with you today 
the correct way to host your static website on AWS S3 with CloudFront. Unlike other blog posts out there, this tutorial
will work all permutations of HTTP, HTTPS, apex domain and www. 

### Configure Route 53

TODO: Write this section

### Create www Bucket

1. Go to S3 Console
2. Click `Create Bucket`
3. Name it something meaningful (e.g. mywebsite)
4. Select a region
5. **Important**: Do not enable static website hosting 

### Create Apex Bucket

1. Go to S3 Console
2. Click `Create Bucket`
3. Name it the root domain of your website (e.g. mywebsite.com)
4. Select a region
5. Click `Properties`
6. Click `Static Website Hosting`
7. Select `Redirect all requests to another host name`
8. Enter in the www host name of your website (e.g. www.mywebsite.com)
9. Click `Permissions` 
10. Click `Add more permissions`
11. Add a new grantee with grantee `Everyone` and select `View Permissions`

### Create www CloudFront Distribution

1. Go to CloudFront Console
2. Click `Create Distribution`
3. **Origin Settings**
    1. `Origin Domain Name`: Set this to <bucket-name>.s3.amazonaws.com (e.g. mywebsite.s3.amazonaws.com)
    2. `Origin Path`: Bar
    3. `Origin ID`: Bar
    <!--4. `Restrict Bucket Access`: No-->
    4. `Origin Custom Headers`: Leave blank
4. **Default Cache Behavior Settings**
    1. Viewer Protocol Policy:
    2. Allowed HTTP Methods: 
    3. Viewer Protocol Policy:
    4. Object Caching: 
    5. Forward Cookies: 
    6. Query String Forwarding and Caching: 
    7. Smooth Streaming: 
    8. Restrict Viewer Access (Use Signed URLs or Signed Cookies): 
    9. Compress Objects Automatically: 
5. **Distribution Settings**
    1. Price Class: 
    2. AWS WAF Web ACL: 
    3. Alternate Domain Names (CNAMEs):
    4. SSL Certificate: 
    5. Supported HTTP Versions: 
    6. Default Root Object: 
    7. Logging: 
    8. Enable IPv6: 
    9. Comment: 
    10. Distribution State: 



### Create Apex CloudFront Distribution




