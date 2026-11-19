# Lab 01: AWS EC2 Apache Troubleshooting

## Project Overview

Hands-on troubleshooting of an Apache web server hosted on an AWS EC2 Ubuntu instance.

This lab covers five practical troubleshooting scenarios involving Linux services, AWS networking, file permissions, Apache configuration and EC2 resource monitoring.

## Environment

| Component | Configuration |
|---|---|
| Cloud Provider | AWS |
| Compute | EC2 |
| Operating System | Ubuntu 24.04 LTS |
| Instance Type | t3.micro |
| Web Server | Apache HTTP Server |
| HTTP Port | TCP 80 |
| Storage | 8 GiB EBS root volume |
| Region | Asia Pacific (Sydney) |

## Lab Incidents


| Incident | Scenario | Result |
|---|---|---|
| 01 | [Apache Service Failure](Incident-01-Apache-Service-Failure.md) | Resolved |
| 02 | [Security Group Blocking HTTP](Incident-02-Security-Group-HTTP-Blocked.md) | Resolved |
| 03 | [HTTP 403 – File Permissions](Incident-03-Apache-File-Permissions-403.md) | Resolved |
| 04 | [Apache Configuration Error](Incident-04-Apache-Configuration-Error.md) | Resolved |
| 05 | [EC2 Resource Monitoring](Incident-05-EC2-Resource-Monitoring.md) | Investigation completed |


## Troubleshooting Skills

- Linux service management using systemctl
- Apache HTTP Server administration
- AWS Security Groups and Network ACLs
- Linux file permissions
- Apache configuration validation
- Linux log investigation
- CPU and memory monitoring
- Disk usage analysis
- Root cause analysis

## Troubleshooting Methodology

1. Understand the reported problem.
2. Collect relevant system information.
3. Investigate the affected infrastructure layer.
4. Identify the root cause.
5. Apply a safe corrective action.
6. Verify the result.

## Project Outcome

Practised investigating common EC2 and Apache issues using Linux commands and AWS networking configurations.

This project demonstrates practical troubleshooting skills relevant to entry-level AWS Cloud Support and Infrastructure Support roles.

*Personal hands-on learning lab. All exercises were conducted in a test AWS environment.*
