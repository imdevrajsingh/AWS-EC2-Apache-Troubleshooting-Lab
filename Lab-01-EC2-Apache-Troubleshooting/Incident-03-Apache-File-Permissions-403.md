# Incident 03: Apache File Permission Error (HTTP 403)

## 1. Problem Statement

While accessing a test webpage hosted on the Apache server, the request returned `HTTP 403 Forbidden` instead of displaying the webpage.

## 2. Environment

- Cloud Provider: AWS
- Compute: EC2
- Operating System: Ubuntu 24.04 LTS
- Web Server: Apache HTTP Server
- Web Root: `/var/www/html/`
- Test Directory: `/var/www/html/lab403/`

## 3. Investigation

Created a test directory:

```bash
sudo mkdir -p /var/www/html/lab403
```

Created an HTML test page:

```bash
echo "<h1>Cloud Support Troubleshooting Lab</h1><p>Testing Apache file permissions.</p>" | sudo tee /var/www/html/lab403/index.html
```

Checked the file permissions:

```bash
ls -l /var/www/html/lab403/index.html
```

The file initially had permissions `644`.

For the controlled failure simulation, removed all permissions:

```bash
sudo chmod 000 /var/www/html/lab403/index.html
```

Tested the webpage locally:

```bash
curl -I http://localhost/lab403/
```

**Observed result:** `HTTP/1.1 403 Forbidden`

## 4. Root Cause Analysis

The Apache process could not read the HTML file because all file permissions had been removed.

Checked the Apache error log:

```bash
sudo tail -n 20 /var/log/apache2/error.log
```

Relevant error:

```text
(13)Permission denied: file permissions deny server access
```

This confirmed that the issue was related to file permissions.

## 5. Resolution

Restored the appropriate file permissions:

```bash
sudo chmod 644 /var/www/html/lab403/index.html
```

Permission explanation:

- Owner: Read and write
- Group: Read
- Others: Read

## 6. Verification

Executed:

```bash
curl -I http://localhost/lab403/
```

**Expected and observed result:** `HTTP/1.1 200 OK`

The test webpage was also verified in the browser.

## 7. Key Learnings

- Understanding Linux file permissions.
- Troubleshooting Apache HTTP 403 errors.
- Using `chmod` to modify permissions.
- Inspecting Apache error logs.
- Understanding the relationship between Linux permissions and web server access.

## Evidence

### Apache HTTP 403 – File Permission Troubleshooting

![Apache 403 Troubleshooting](screenshots/EC2%20Apache%20403%20Troubleshooting%20Dashboard.png)


**Status:** Successfully resolved in the practice environment.
