---
title: "Scheduling EC2 Instances using Lambda and CloudWatch Events"
link: http://tech.mybuilder.com/scheduling-ec2-instances-using-lambda-and-cloudwatch-events/
meta: "Looking into Scheduling EC2 Instances using Lambda and CloudWatch Events"
---

Over the past couple of months MyBuilder has be transitioning from primarily a dedicated server-stack (with orchestration through [Puppet](https://puppet.com/)) to cloud infrastructure by-way of [Amazon Web Services](https://aws.amazon.com/).
We have been a proponent of AWS for quite some time, taking advantage of services such as S3 and CloudFront in our current setup.
We are also not unfamiliar with EC2, spreading some of our application requirements onto several instances over the past couple of years.
However, we really have not been taking full advantage of the 'Cloud nature' of the product, and still treating each server as something in-between a [Snowflake](https://martinfowler.com/bliki/SnowflakeServer.html) and [Phoenix](https://martinfowler.com/bliki/PhoenixServer.html).
<!--more-->