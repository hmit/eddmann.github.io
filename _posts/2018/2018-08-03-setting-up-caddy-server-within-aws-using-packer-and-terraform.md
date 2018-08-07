---
title: "Setting up Caddy Server within AWS using Packer and Terraform"
link: https://tech.mybuilder.com/setting-up-caddy-server-within-aws-using-packer-and-terraform/
meta: "Setting up Caddy Server within AWS using Packer and Terraform"
---

With the [recent update](https://security.googleblog.com/2018/02/a-secure-web-is-here-to-stay.html) to Google Chrome helping shape a more secure Web by marking all HTTP sites as "not secure", I thought it was time that I make the necessary changes to how we host audio files for the [Three Devs and a Maybe](https://threedevsandamaybe.com/) podcast.
In this post I would like to discuss setting up [Caddy Server](https://caddyserver.com/) (which provides HTTPS out of the box!) as a static-hosting platform on AWS - provisioning the instance with Packer and the surrounding infrastructure using Terraform.
<!--more-->
