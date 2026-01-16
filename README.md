# Web Application Incident Response & Network Traffic Analysis

## Overview
This project documents a SOC-style incident response investigation involving
a compromised web application and post-exploitation network activity.

## Key Findings
- Insecure file upload via `/reviews/upload.php`
- Malicious PHP file disguised as an image (`image.jpg.php`)
- Web-accessible and executable `/uploads/` directory
- Outbound command-and-control traffic on TCP port 8080
- Attempted access to sensitive system files

## Tools Used
- Wireshark
- HTTP traffic analysis
- Manual packet inspection

## Disclaimer
All analysis was conducted in a controlled lab or simulated environment.
