# Incident 02: AWS Security Group Blocking HTTP

## 1. Problem Statement

The Apache website was accessible locally on the EC2 instance but could not be accessed from an external browser.

## 2. Environment

- Cloud Provider: AWS
- Compute: EC2
- Operating System: Ubuntu 24.04 LTS
- Web Server: Apache HTTP Server
- Protocol: HTTP
- Port: TCP 80

## 3. Investigation

First, checked whether Apache was running:

```bash
sudo systemctl status apache2
```

Verified that Apache was listening on port 80:

```bash
sudo ss -tlnp | grep :80
```

Tested local connectivity:

```bash
curl -I http://localhost
```

The local request returned HTTP 200 OK.

Also inspected the host firewall:

```bash
sudo ufw status verbose
```

The UFW firewall was inactive.

Inspected the AWS Security Group inbound rules and Network ACL configuration.

## 4. Root Cause

During the controlled troubleshooting exercise, the inbound HTTP rule for TCP port 80 was removed from the EC2 Security Group.

As a result, external HTTP traffic could not reach the Apache server, although local connectivity continued working.

## 5. Resolution

Restored the inbound Security Group rule:

| Type | Protocol | Port | Source |
|---|---|---|---|
| HTTP | TCP | 80 | 0.0.0.0/0 |

The SSH rule remained restricted to My IP.

## 6. Verification

- Confirmed Apache was running.
- Confirmed port 80 was listening.
- Restored the inbound HTTP rule.
- Verified that external browser access was restored.

## 7. Key Learnings

- Understanding AWS Security Group inbound rules.
- Distinguishing local connectivity from external connectivity.
- Understanding the role of Network ACLs.
- Troubleshooting HTTP connectivity at the AWS network layer.
- Using a layered troubleshooting approach.

## Evidence

### AWS Security Group HTTP Troubleshooting

![AWS Security Group HTTP Troubleshooting](screenshots/AWS%20Security%20Group%20HTTP%20Troubleshooting%20Dashboard.png)

**Status:** Successfully resolved in the practice environment.

**Status:** Successfully resolved in the practice environment.
