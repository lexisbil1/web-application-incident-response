# Indicators of Compromise (IOCs)

This document lists indicators identified during the investigation of the web
application compromise. These indicators can be used for detection, alerting,
and threat-hunting activities.

---

## Network Indicators

| Indicator Type | Value | Description |
|---------------|-------|-------------|
| Outbound Port | TCP 8080 | Reverse-shell / C2 communication |
| Traffic Direction | Server → External | Unauthorized outbound connection |
| Protocol | TCP | Non-standard egress traffic |

---

## File-Based Indicators

| Indicator Type | Value | Description |
|---------------|-------|-------------|
| Malicious File | `image.jpg.php` | PHP payload disguised as image |
| Web Shell | `c99.php` | Remote command execution tool |
| Upload Directory | `/uploads/` | Web-accessible executable directory |

---

## Application Indicators

| Indicator Type | Value | Description |
|---------------|-------|-------------|
| Upload Endpoint | `/reviews/upload.php` | Vulnerable file upload handler |
| Access Pattern | Direct access to uploaded files | Indicates code execution |
| HTTP Method | POST | Used for malicious file upload |

---

## Host-Based Indicators

| Indicator Type | Value | Description |
|---------------|-------|-------------|
| Target File | `/etc/passwd` | Sensitive file accessed post-exploitation |
| Execution Behavior | PHP code execution | Unauthorized server-side execution |

---

## Timeline Correlation

The indicators above correlate with the reconstructed attack timeline and confirm
successful exploitation followed by post-exploitation activity and remote access.

---

## Recommended Usage

- Add network indicators to firewall and IDS/IPS rules
- Monitor file indicators via host-based intrusion detection
- Use application indicators for WAF tuning and log correlation
- Incorporate IOCs into threat-hunting workflows
