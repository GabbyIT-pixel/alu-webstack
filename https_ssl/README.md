# HTTPS SSL

## Description

This project covers the concepts of HTTPS, SSL termination, and domain configuration using HAProxy as a load balancer with SSL/TLS support.

## Background Context

What happens when you don't secure your website traffic? All data sent over HTTP is transmitted in plain text — anyone on the network can intercept and read it. HTTPS solves this by encrypting traffic using SSL/TLS.

## Learning Objectives

- What are the 2 main roles of HTTPS SSL:
  1. **Encryption** – Protects data in transit from eavesdropping
  2. **Authentication** – Verifies that you are communicating with the intended server
- What is the purpose of encrypting traffic
- What SSL termination means

## Infrastructure

| Server Name  | IP Address      | Role              |
|--------------|-----------------|-------------------|
| 6983-web-01  | 54.227.215.118  | Web Server        |
| 6983-web-02  | 3.83.142.166    | Web Server        |
| 6983-lb-01   | 98.81.221.12    | Load Balancer     |

## Domain

- Domain: `gabrielmugisha.tech`
- Subdomains configured:
  - `www` → lb-01 (98.81.221.12)
  - `lb-01` → lb-01 (98.81.221.12)
  - `web-01` → web-01 (54.227.215.118)
  - `web-02` → web-02 (3.83.142.166)

## Files

| File | Description |
|------|-------------|
| `0-world_wide_web` | Bash script that audits DNS subdomains |
| `1-haproxy_ssl_termination` | HAProxy configuration with SSL termination |

## Requirements

- Ubuntu 16.04 LTS
- HAProxy 1.5+
- Certbot (Let's Encrypt) for SSL certificate
- All Bash scripts pass Shellcheck 0.3.7

## Usage

### Task 0 – World Wide Web

```bash
# Audit all default subdomains
./0-world_wide_web gabrielmugisha.tech

# Audit a specific subdomain
./0-world_wide_web gabrielmugisha.tech web-02
```

### Task 1 – HAProxy SSL Termination

```bash
# Copy config to HAProxy and reload
sudo cp 1-haproxy_ssl_termination /etc/haproxy/haproxy.cfg
sudo service haproxy reload

# Test HTTPS
curl -sI https://www.gabrielmugisha.tech
```
