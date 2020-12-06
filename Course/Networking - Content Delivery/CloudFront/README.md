## [CloudFront](https://aws.amazon.com/cloudfront/)


### [What's a CDN](https://www.cloudflare.com/learning/cdn/what-is-a-cdn/)

* A content delivery network or content distribution network is a geographically distributed network of proxy servers and their data centres

* Key terminology about CloudFront:
  * Edge Location: Is the location where the content is cached (separate from AWS AZ's or regions)
    Be aware that you can also write on edge locations, is not ready only.
  * Invalidating (erasing) the cache costs money.
  * Origin: Is the source of the files the CDN will distribute. An origin can be an EC2 instance, an S3 bucket, an Elastic Load Balancer or Route53, you can also have your own origin, it not mandatory that is within AWS.
  * Distribution: Is the name AWS calls CDN's.
    * You can Have two types: Web that is for generic web contents and RTMP that is for video streaming
    * TTL: time to live of the cached object.

* CloudFront & CloudFront Signed URL
    - Edge Location - This is the location where content will be cached. This is a different than an AWS Region/AZ
     - Distribution - This is the name given the CDN, which consists of collection of edge locations
     - Origin - This is the origin of all the files that CDN will distribute. This can be either an S3 bucket, an EC2 instance, an Elastic Load Balancer, or Route 53
     - Web Distribution - Typically used for websites
     - RTMP - Used for media Streaming
     - Signed URL v/s Cookies 
        * A signed cookie or URL is used for providing access to premium content / paid users / authorized users
        * A signed URL is for individual file
        * A signed cookie is for multiple files
        * While creating a signed URl or Cookie we can attach a policy. A policy includes - URL Expiration, IP ranges & Trusted Signers (Which AWS accounts can create signed URL's)
        * If the origin is EC2 then use CloudFront signed URL and if the origin is S3 then use S3 signed URL