# 0x0F. HTTPS SSL

This project configures a domain with DNS records, then secures the website with HTTPS by terminating SSL on HAProxy.

## Description

The domain `abdikarim.tech` points to a load balancer (lb-01) that distributes traffic between two web servers (web-01 and web-02). Each task builds on the one before:

- DNS: subdomains `www`, `lb-01`, `web-01` and `web-02` are A records pointing to the right servers.
- SSL termination: HAProxy receives encrypted traffic on port 443, decrypts it and passes it to the web servers.
- Redirect: HAProxy sends all HTTP traffic to HTTPS with a 301.

## Files

| File | Description |
|---|---|
| `0-world_wide_web` | Bash script that displays the record type and destination of the subdomains of a domain |
| `1-haproxy_ssl_termination` | HAProxy configuration that accepts HTTPS traffic on port 443 |
| `2-redirect_http_to_https` | HAProxy configuration that redirects HTTP to HTTPS with a 301 |

## Usage

### 0-world_wide_web

```bash
./0-world_wide_web <domain> [subdomain]
```

- With only a domain, it shows `www`, `lb-01`, `web-01` and `web-02`, in that order.
- With a domain and a subdomain, it shows only that subdomain.

Example:

```
$ ./0-world_wide_web abdikarim.tech
The subdomain www is a A record and points to 18.175.145.68
The subdomain lb-01 is a A record and points to 18.175.145.68
The subdomain web-01 is a A record and points to 35.178.171.253
The subdomain web-02 is a A record and points to 3.10.171.138

$ ./0-world_wide_web abdikarim.tech web-02
The subdomain web-02 is a A record and points to 3.10.171.138
```

The script needs the `dig` command. On Ubuntu, install it with `sudo apt-get install -y dnsutils`.

## Requirements

- Ubuntu 20.04 LTS
- Scripts are written in Bash and start with `#!/usr/bin/env bash`
- Files end with a new line
- Scripts are executable (`chmod +x`)
- `0-world_wide_web` uses `awk` and at least one Bash function, and ignores shellcheck SC2086

## Author

Abdikarim
