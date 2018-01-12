---
title: "Unlocking the AWS WAF Logs"
link: http://tech.mybuilder.com/unlocking-the-aws-waf-logs/
meta: "Unlocking the AWS WAF Logs using Serverless, Lambda and AWS SDK"
---

In this article we discuss our recent move to route all requests through [CloudFront](https://aws.amazon.com/cloudfront/), allowing us to parse all traffic through the [AWS Web Application Firewall](https://aws.amazon.com/waf/) (WAF).
We highlight the reasoning behind this change, and some issues/remedies ecountered when trying to garner concrete logs from the WAF instance.
<!--more-->