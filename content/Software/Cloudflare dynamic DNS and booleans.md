---
id: 8nkmmjukav
slug: cloudflare-dynamic-dns-and-booleans
title: Cloudflare dynamic DNS and booleans
created: 2025-02-25 09:31:17
updated: 2025-02-25 09:28:14
tags:
  - perl
  - cloudflare
  - software
---
[Cloudflare](https://www.cloudflare.com/) has an [API that allows DNS records to be updated](https://developers.cloudflare.com/api/resources/dns/subresources/records/methods/update/) — assuming you use Cloudflare to *manage* your DNS records. 

If not, look away now.

Using `curl` you make a PUT request to a particular URL, supplying authentication details in the form of an email and the API key. There are further details online; for example, [here](https://bytefreaks.net/gnulinux/bash/cloudflare-api-dns-update). 

Part of the request is submitted in JSON format. Not a problem *except* for the need to submit a boolean `true` value for one of the records. This turned out to be more problematic than I expected using Perl.

I use the [JSON::Tiny module](https://metacpan.org/dist/JSON-Tiny/view/lib/JSON/Tiny.pod) to convert a hash (key-value pairs) of data into JSON format to append to the PUT request. Any variant of 'true', escaped or not, caused Cloudflare to 'barf' and reject the dynamic DNS update.

## And the answer is …

Use `\1` as the value, which (together with `\0`) is a *scalar reference*, that indicates boolean `true` (and, for `\0` … `false`, obviously).

So you start with a hash that looks something like this (some authentication bits removed for security):

```
my %json = (
  content => $ip,
  name    => 'geekery.theapiarist.org',
  proxied => \1,
  type    => 'A',
  comment => $comment,
  tags    => [],
  ttl     => 3600,
);
```

which, when dealt with by `encode_json`, returns:

```
{"comment":"Updated","content":"123.456.789.123","name":"geekery.theapiarist.org","proxied":true,"tags":[],"ttl":3600,"type":"A"}
```

Note the absence of quoting on the proxied entry.

Simple when you know how, which I didn't 😞, which is why it took me an hour and some Google-*fu* to [find the answer](https://stackoverflow.com/questions/43867553/how-to-send-boolean-value-from-perl-script-without-converting-them-into-string).