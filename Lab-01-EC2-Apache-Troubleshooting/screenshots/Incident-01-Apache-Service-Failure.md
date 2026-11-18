# Incident 01: Apache Service Failure

## 1. Problem Statement

The Apache-hosted website became inaccessible because the Apache web server service was stopped.

## 2. Environment

- Cloud: AWS EC2
- Operating System: Ubuntu 24.04 LTS
- Web Server: Apache HTTP Server
- HTTP Port: 80

## 3. Investigation

Checked the Apache service status:

```bash
sudo systemctl status apache2
```

The service showed:

```text
Active: inactive (dead)
```

This confirmed that Apache was not running.

## 4. Root Cause

The Apache service had been deliberately stopped as part of this troubleshooting exercise.

## 5. Resolution

Started the Apache service:

```bash
sudo systemctl start apache2
```

## 6. Verification

Checked the service status again:

```bash
sudo systemctl status apache2
```

Tested the local HTTP response:

```bash
curl -I http://localhost
```

Expected successful response:

```text
HTTP/1.1 200 OK
```

## 7. Key Learnings

- Checking Linux services with systemctl.
- Understanding Apache service states.
- Starting a stopped web server.
- Verifying service recovery using curl.

**Status:** Successfully resolved in the practice environment.
