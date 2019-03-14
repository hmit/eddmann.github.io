---
title: "Setting up GitHub Pages HTTPS Custom Domains using CloudFront and Lambda@Edge"
link: https://tech.mybuilder.com/setting-up-github-pages-https-custom-domains-using-cloudfront-and-lambda-edge/
meta: "Setting up GitHub Pages HTTPS Custom Domains using CloudFront and Lambda@Edge"
---

We recently wished to switch over our sites hosted on [GitHub Pages](https://pages.github.com/) to be soley HTTPS.
However, although you are able to supply a [custom domain](https://help.github.com/articles/using-a-custom-domain-with-github-pages/) or support [HTTPS traffic](https://github.com/blog/2186-https-for-github-pages) you are not able to do both.
In this article I would like to guide you through the process of how we went about achieving this using [CloudFront](https://aws.amazon.com/cloudfront/), [Route 53](https://aws.amazon.com/route53/) and [Lambda@Edge](https://aws.amazon.com/lambda/edge/).
<!--more-->
