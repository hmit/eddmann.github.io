---
layout: post
title: "Self-Signed SSL Certificates with Nginx and Apache"
meta: "Creating and configuring self-signed certificates with Nginx and Apache."
---

Since having the opportunity to discuss web application security ([part 1](http://threedevsandamaybe.com/posts/web-application-security-part-1/), [part 2](http://threedevsandamaybe.com/posts/web-application-security-part-2/)) recently on the podcast, I thought it was a good time to have a deeper look into SSL/TLS (Transport Layer Security).
There are plenty of good resources online discussing the [technical side](http://www.youtube.com/watch?v=iQsKdtjwtYI) of the topic, however, at a high-level point-to-point encryption and server identification are the two problems it attempts to solve.
<!--more-->

Self-signed SSL certificates are an inexpensive (free) means of taking advantage of point-to-point encryption on non-production, development server setups.
The caveat to this is that visiting browsers will warn the user that the certificate should not be trusted, as it has been self-signed.
If you require a trusted certificate for a production application, you are required to purchase a certificate from a reputable CA (Certificate Authority) to verify your identity.

## Creating the Self-Signed Certificate

The examples in this post will directed at a CentOS setup, however, they should not differ much for other distributions.
First we are required to create a private key to sign the certificate that will be used for visiting users.
I have decided to use strong encryption (4096 bits, this can be lowered) and make the certificate valid for a year from creation.
So as to allow the command to run in non-interactive mode I have supplied the certificate details that are required using the 'subj' option.

{% highlight bash %}
$ openssl req -newkey rsa:4096 -days 365 -nodes -x509 \
    -subj "/C=GB/ST=London/L=Fulham/O=Local/OU=Development/CN=local.dev/emailAddress=email@local.dev" \
    -keyout local.dev.key \
    -out local.dev.crt
{% endhighlight %}

We can now move the certificate and private key to the desired location and tighten up file permissions on the two files.

{% highlight bash %}
$ cp local.dev.crt /etc/ssl/certs/
$ cp local.dev.key /etc/ssl/private/
$ chmod 600 /etc/ssl/certs/local.dev.crt /etc/ssl/private/local.dev.key
{% endhighlight %}

## Apache Configuration

Now that we have generated the private key and certificate we must next make sure that the SSL module is present and enabled in the Apache installation.

{% highlight bash %}
$ yum install mod_ssl
{% endhighlight %}

With the prerequisites out of the way we are now able to direct access through port 443 (HTTPS) to use the generated certificate.

{% highlight apache %}
<VirtualHost *:443>

    SSLEngine On
    SSLCertificateFile /etc/ssl/certs/local.dev.crt
    SSLCertificateKeyFile /etc/ssl/private/local.dev.key

    # ...

</VirtualHost>
{% endhighlight %}

Optional, we can also force all traffic sent and received be over HTTPS by redirecting HTTP requests to use the secure connection.

{% highlight apache %}
<VirtualHost *:80>

   Redirect permanent / https://www.example.com/

   # ...

</VirtualHost>
{% endhighlight %}

## Nginx Configuration

With a similar process as the Apache configuration we can configure Nginx to use the generated certificate when accessed over port 443.

{% highlight nginx %}
server {

    listen 443;

    ssl on;
    ssl_certificate /etc/ssl/certs/local.dev.crt;
    ssl_certificate_key /etc/ssl/private/local.dev.key;

    # ...

}
{% endhighlight %}

Optional, if you wish all traffic to be transported through HTTPS we can setup a permanent redirect on port 80.

{% highlight nginx %}
server {

    listen 80;

    return 301 https://$host$request_uri;

}
{% endhighlight %}