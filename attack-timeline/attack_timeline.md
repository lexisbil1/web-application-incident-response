# Attack Timeline (Reconstructed)

The following timeline was reconstructed through analysis of captured network traffic,
HTTP request inspection, and correlation of server responses. All timestamps are
approximate and recorded in GMT.

## Timeline of Events

| Time (GMT) | Event |
|-----------|------|
| 18:43:30 | Automated HTTP reconnaissance begins |
| 18:43:50 | Suspicious User-Agent observed in HTTP requests |
| 18:43:57 | Vulnerable file upload directory identified |
| 18:44:19 | Malicious file upload request initiated |
| 18:44:25 | Web shell (`c99.php`) successfully uploaded |
| 18:44:35 | Web shell accessed via `/uploads/` directory |
| 18:44:45 | Outbound reverse-shell traffic detected on TCP port 8080 |
| 18:46:39 | Attempted access to sensitive system file `/etc/passwd` |
| 18:47:52 | Suspicious file and abnormal activity identified by Development team |

## Analysis Summary

The timeline shows a rapid transition from automated reconnaissance to successful
exploitation and post-exploitation activity. Initial automated scanning was followed
by identification of an insecure file upload mechanism, allowing the attacker to
upload and execute a PHP-based web shell.

Subsequent outbound network traffic confirms command-and-control communication,
indicating active remote access to the compromised server. Attempts to access
sensitive system files further demonstrate post-exploitation reconnaissance.

This sequence of events highlights the impact of insufficient input validation,
improper file execution controls, and lack of outbound traffic monitoring.
