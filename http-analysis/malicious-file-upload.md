# Malicious File Upload Analysis

## Overview
This analysis documents the discovery and exploitation of an insecure file upload
functionality within the web application. Network traffic inspection confirms that
an attacker successfully uploaded a malicious PHP file disguised as an image, leading
to remote command execution on the server.

---

## POST Request Summary

The attacker issued an HTTP POST request to the application’s upload endpoint using
`multipart/form-data`. The request included a malicious file with a misleading filename
extension intended to bypass basic validation controls.

**Request Details:**
- HTTP Method: POST
- Endpoint: `/reviews/upload.php`
- Content-Type: `multipart/form-data`
- Uploaded Filename: `image.jpg.php`
- Declared MIME Type: `application/x-php`

The server responded with an HTTP 200 status code and a success message, confirming that
the file was accepted and stored on the server.

---

## Identified Upload Weakness

Analysis indicates multiple security control failures within the upload functionality:

- Lack of file extension validation (double extensions allowed)
- Absence of MIME-type enforcement on uploaded files
- Uploaded files stored in a web-accessible directory
- No execution restrictions applied to the upload directory
- No server-side sanitization or renaming of uploaded files

These weaknesses allowed the attacker to upload and later execute arbitrary PHP code.

---

## Why This Is Dangerous

Insecure file upload vulnerabilities are considered high-risk because they can lead
directly to full system compromise. In this case, the attacker was able to:

- Execute arbitrary commands on the web server
- Establish outbound reverse-shell communication
- Perform post-exploitation reconnaissance
- Access sensitive system files such as `/etc/passwd`

Without proper restrictions, an attacker can use such access to escalate privileges,
deploy persistent backdoors, or pivot further into the internal network.

---

## Security Impact

- Remote Code Execution (RCE)
- Loss of system integrity
- Potential data exposure
- Risk of lateral movement within the environment

---

## Mitigation Recommendations

- Enforce strict allowlists for file extensions and MIME types
- Store uploaded files outside web-accessible directories
- Disable script execution within upload directories
- Implement server-side file renaming
- Monitor and restrict outbound network connections
- Apply web application firewall (WAF) rules for upload endpoints
