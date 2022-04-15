# Misc
## Multi-Domain Certificates 
The Subject Alternative Name field lets you specify additional host names (sites, IP addresses, common names, etc.) to be protected by a single SSL Certificate, such as a Multi-Domain (SAN) or Extend Validation Multi-Domain Certificate.

**Secure Host Names on Different Base Domains in One SSL Certificate:** A Wildcard Certificate can protect all first-level subdomains on an entire domain, such as _*.example.com_. However, a Wildcard Certificate **cannot** protect both _www.example.com_ and _www.example.net_.

**Virtual Host Multiple SSL Sites on a Single IP Address:** Hosting multiple SSL-enabled sites on a single server typically requires a unique IP address per site, but a Multi-Domain (SAN) Certificate with Subject Alternative Names can solve this problem. Microsoft IIS and Apache are both able to Virtual Host HTTPS sites using [Multi-Domain (SAN) Certificates](https://www.digicert.com/tls-ssl/multi-domain-ssl-certificates).

**Greatly Simplify Your Server's SSL Configuration:** Using a Multi-Domain (SAN) Certificate saves you the hassle and time involved in configuring multiple IP addresses on your server, binding each IP address to a different certificate, and trying to piece it all together.