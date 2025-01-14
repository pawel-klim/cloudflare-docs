---
_build:
  publishResources: false
  render: never
  list: never
---

Non-wildcard hostname certificates will automatically renew as long as every hostname on the certificate is proxying traffic through Cloudflare.

However, if one or more of the hostnames on the certificate is not proxying through Cloudflare, the certificate will not issue and you will be required to complete DCV for each hostname not proxied - which will require manually updating the DCV token or proxying the hostname - in order for the certificate to renew.

Wildcard hostname certificates will be required to use [TXT based DCV](/ssl/edge-certificates/changing-dcv-method/methods/txt/) for renewals of the certificate. You will need to place one TXT DCV token for every hostname on the certificate for it to successfully renew. If one or more of the hostnames on the certificate fail to validate, the certificate will not be renewed.

This means that a wildcard certificate covering `example.com` and `*.example.com` will require two DCV tokens to be placed at the authoritative DNS provider. Similarly, a certificate with five hostnames in the SAN (including a wildcard) will require five DCV tokens to be placed at the authoritative DNS provider. 