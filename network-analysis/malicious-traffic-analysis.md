# Malicious Network Traffic Analysis

## Overview
This section documents the identification and analysis of suspicious outbound network
traffic originating from the compromised web server. Packet inspection revealed
post-exploitation command-and-control (C2) communication following a successful
malicious file upload.

---

## TCP 8080 Detection

Outbound TCP connections were observed from the web server to an external IP address
over TCP port **8080** shortly after the malicious file upload and execution.

Port 8080 is commonly used for alternative HTTP services but is frequently abused by
attackers to bypass restrictive firewall rules and establish reverse-shell or
command-and-control communication.

The timing of the traffic directly correlates with access to the uploaded web shell,
indicating active remote control of the compromised system.

---

## Wireshark Filters Used

The following Wireshark filters were applied to isolate the suspicious traffic:

- `tcp.port == 8080`
- `tcp.flags.syn == 1 && tcp.flags.ack == 0`
- `ip.src == <web_server_ip> && tcp.port == 8080`

These filters allowed identification of outbound connection attempts initiated by the
server rather than inbound client requests.

---

## Why This Indicates Command-and-Control Activity

Several indicators strongly suggest command-and-control behavior:

- The connection was **initiated by the server**, not an external client
- The destination was an **external, non-trusted IP address**
- The traffic occurred **immediately after web shell execution**
- TCP port 8080 is commonly associated with reverse shells and backdoor callbacks
- No legitimate application service was expected to initiate outbound connections on
  this port

Together, these factors confirm post-exploitation activity and remote attacker control.

---

## Security Impact

- Unauthorized outbound communication
- Loss of control over the compromised host
- Potential data exfiltration
- Risk of lateral movement within the network

---

## Detection and Mitigation Recommendations

- Implement strict outbound firewall rules
- Monitor egress traffic for uncommon ports
- Deploy IDS/IPS signatures for reverse-shell patterns
- Enable logging and alerting on abnormal outbound connections
- Regularly audit server network behavior baselines
