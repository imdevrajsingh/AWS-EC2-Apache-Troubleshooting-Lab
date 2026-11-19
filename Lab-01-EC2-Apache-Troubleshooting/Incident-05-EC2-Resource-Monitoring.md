# Incident 05: AWS EC2 Resource Monitoring and Troubleshooting

## 1. Incident Overview

**Incident ID:** 05  
**Incident Category:** EC2 Resource Monitoring  
**Cloud Provider:** Amazon Web Services (AWS)  
**Compute Service:** Amazon EC2  
**Operating System:** Ubuntu 24.04.5 LTS  
**Instance Type:** t3.micro  
**Region:** Asia Pacific (Sydney)

## 2. Problem Statement

The objective of this exercise was to investigate the resource utilization of an AWS EC2 instance.

The investigation focused on CPU utilization, memory consumption and disk capacity to understand how resource constraints can affect server performance and application availability.

This exercise demonstrates a systematic approach to Linux resource monitoring and infrastructure troubleshooting.

## 3. EC2 Environment Details

| Component | Configuration |
|---|---|
| Cloud Provider | AWS |
| Service | EC2 |
| Operating System | Ubuntu 24.04.5 LTS |
| Instance Type | t3.micro |
| vCPU | 2 |
| Memory | Approximately 1 GiB |
| Root Volume | 8 GiB gp3 |
| Region | ap-southeast-2 (Sydney) |

## 4. CPU Investigation

### Command Used

```bash
top
```

### Investigation Objective

- Observe running processes.
- Identify processes consuming high CPU.
- Check CPU utilization and idle percentage.
- Review system load averages.

### Findings

- CPU idle percentage: Approximately 99.7%
- Load average: 0.01, 0.02, 0.00
- No unusually high CPU-consuming process was identified in the observed output.

**Result:** CPU utilization was low during the monitoring snapshot.


## 5. Memory Investigation

### Command Used

```bash
free -h
```

The `top` command can also be used to observe memory consumption and process-level usage.

### Investigation Objective

- Check total memory.
- Identify used and available memory.
- Understand memory consumption.
- Identify possible memory pressure.


### Findings

- Total memory: 909 MiB
- Used memory: Approximately 300 MiB
- Free memory: 304 MiB
- Buff/cache: 415 MiB
- Available memory: 609 MiB
- Swap: 0

**Result:** The system had approximately 609 MiB of available memory during the observed snapshot.

## 6. Disk Investigation

### Command Used

```bash
df -h
```

### Investigation Objective

- Check filesystem capacity.
- Identify used and available disk space.
- Review filesystem utilization percentages.
- Identify filesystems approaching capacity.

### Findings

- Root filesystem: /dev/root
- Total size: 6.8 GB
- Used space: 2.7 GB
- Available space: 4.1 GB
- Utilization: 40%

**Result:** The root filesystem had approximately 4.1 GB of available space.

## 7. Output and Findings

Summarize the evidence collected during the investigation.

| Resource | Command | Finding |
|---|---|---|
| CPU | `top` | Approximately 99.7% idle; low load average |
| Memory | `free -h` | 609 MiB available; 0 swap |
| Disk | `df -h` | 40% utilized; 4.1 GB available |

## 8. Root Cause Analysis

No specific CPU, memory or disk-related failure should be declared unless supported by the collected evidence.

If resource pressure is identified, document the affected resource, supporting output and the process or filesystem responsible.

**Current status:** No confirmed resource-related root cause documented.

## 9. Recommended Corrective Actions

Depending on the investigation findings:

- **High CPU:** Identify the resource-intensive process and investigate why it is consuming CPU.
- **High memory usage:** Identify memory-intensive processes and investigate possible memory leaks or insufficient capacity.
- **Low disk space:** Identify large files, logs or unnecessary data before safely freeing disk space.
- **Insufficient instance capacity:** Evaluate whether the workload requires a larger EC2 instance.

Do not terminate processes, delete files or resize resources without validating the impact.

## 10. Verification

After any corrective action:

- Re-run `top` to check CPU utilization.
- Re-run `free -h` to check memory availability.
- Re-run `df -h` to verify filesystem capacity.
- Confirm that the application and required services remain operational.

**Verification status:** Pending evidence of an actual issue and corrective action.

## 11. Key Learnings

- Monitor Linux CPU utilization using `top`.
- Understand CPU idle percentage and load averages.
- Inspect memory usage using `free -h`.
- Understand the difference between free and available memory.
- Monitor filesystem capacity using `df -h`.
- Identify potential resource bottlenecks.
- Use actual system evidence before determining root cause.
- Verify system health after applying corrective actions.

## 12.  Evidence

### Incident 05 – EC2 Resource Monitoring Summary

![EC2 Resource Monitoring Dashboard](screenshots/AWS%20EC2%20Resource%20Monitoring%20Dashboard.png)

> **Note:** This dashboard is an illustrative visualization created for documentation purposes. Its displayed values are not a verbatim capture of the original terminal output. Refer to the documented investigation results for verified observations.

## Final Status

**Documentation:** Completed

**CPU investigation:** Completed

**Memory investigation:** Completed

**Disk investigation:** Completed

**Root cause:** Not established

**Corrective action:** Not required; no confirmed resource issue identified

This incident demonstrates the process of monitoring EC2 resources and investigating potential infrastructure performance issues using Linux commands.
