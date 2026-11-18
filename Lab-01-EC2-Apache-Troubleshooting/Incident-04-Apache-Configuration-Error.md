# Incident 04: Apache Configuration Error Troubleshooting

## 1. Incident Overview

**Incident:** Apache Configuration Validation Failure  
**Cloud Provider:** AWS  
**Compute:** Amazon EC2  
**Operating System:** Ubuntu 24.04.5 LTS  
**Web Server:** Apache HTTP Server 2.4  
**Configuration Test:** Isolated test configuration file

This exercise demonstrates how to identify an invalid Apache configuration directive, inspect the syntax error, correct the test configuration, and validate the result.

## 2. Problem Statement

An isolated Apache configuration test file was created containing an invalid directive.

The objective was to identify the invalid directive using Apache configuration validation tools and correct the test file without modifying the active Apache configuration.

## 3. Investigation and Troubleshooting

### Step 1: Create a test directory

```bash
sudo mkdir -p /tmp/lab4
```

This created a separate directory for the configuration testing exercise.

### Step 2: Create a configuration file containing an invalid directive

```bash
echo "InvalidDirective On" | sudo tee /tmp/lab4/lab4-test.conf
```

The file contained:

```apache
InvalidDirective On
```

### Step 3: Run the standard Apache configuration test

```bash
sudo apachectl configtest
```

**Output:**

```text
Syntax OK
```

The standard test returned successfully because the temporary test file was not part of Apache's active configuration.

### Step 4: Include the test file during configuration validation

```bash
sudo apachectl -t -C "Include /tmp/lab4/lab4-test.conf"
```

**Observed error:**

```text
AH00526: Syntax error on line 1 of /tmp/lab4/lab4-test.conf:
Invalid command 'InvalidDirective'
```

This confirmed that Apache could not recognize the directive in the test configuration file.

## 4. Root Cause Analysis

The root cause was an invalid Apache configuration directive:

```apache
InvalidDirective On
```

Apache configuration files must contain valid directives supported by Apache and its loaded modules.

## 5. Corrective Action

Replaced the invalid directive with a valid configuration directive:

```bash
echo "ServerName localhost" | sudo tee /tmp/lab4/lab4-test.conf
```

The corrected test file contained:

```apache
ServerName localhost
```

## 6. Verification

### Step 1: Validate the corrected configuration

```bash
sudo apachectl -t -C "Include /tmp/lab4/lab4-test.conf"
```

**Output:**

```text
Syntax OK
```

### Step 2: Verify the existing test webpage

```bash
curl -I http://localhost/lab403/
```

**Observed response:**

```text
HTTP/1.1 200 OK
Server: Apache/2.4.58 (Ubuntu)
Content-Type: text/html
```

The existing test webpage remained accessible.

## 7. Key Learnings

- Understand the purpose of Apache configuration validation.
- Identify invalid configuration directives.
- Use `apachectl -t` to validate Apache configuration syntax.
- Use the `Include` directive to test an additional configuration file.
- Understand why an isolated configuration file is not automatically checked by the standard configuration test.
- Correct configuration errors and validate the result.
- Verify HTTP responses using `curl`.

## 8. Important Technical Note

This exercise validated an isolated configuration file. It did not demonstrate an actual Apache service outage or a failed production reload.

A configuration syntax error can prevent Apache from starting or successfully reloading when that invalid configuration is part of the active configuration tree.

No active Apache configuration was intentionally modified during this exercise.

## 9. Final Status

**Status:** Configuration error identified, corrected, and successfully validated in the practice environment.

The corrected test configuration returned `Syntax OK`, and the existing test webpage returned HTTP 200 OK.

## 10. Evidence

Terminal screenshots showing:

1. Creation of the invalid configuration file.
2. Detection of the invalid directive.
3. Correction of the test configuration.
4. Successful syntax validation.
5. HTTP 200 OK verification.

