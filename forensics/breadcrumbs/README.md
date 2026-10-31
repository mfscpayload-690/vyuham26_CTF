# Breadcrumbs

- **Category:** Forensics
- **Points:** 50
- **Status:** Solved
- **Timestamp:** October 31, 2026 &mdash; 15:37:00 IST
- **Flag:** `CTF{cl34rt3xt_cr3ds_0n_th3_w1r3}`

---

## 1. Challenge Overview

A packet capture (`breadcrumbs.pcap`) was captured from an internal corporate network segment where an automated service account was making routine HTTP requests against internal endpoints.

```
IP 10.0.0.5 -> 10.0.0.9:80 (HTTP)
Host: intranet.corp
```

## 2. Forensic Analysis

Inspecting the packet stream using `tshark` / `tcpdump`:

```bash
tcpdump -A -nn -r breadcrumbs.pcap 'tcp[tcpflags] & tcp-push != 0'
```

Filtering for HTTP header patterns reveals unencrypted `GET` requests issued across various paths (`/`, `/about`, `/css/site.css`, `/img/logo.png`, `/login`, `/api/status`, `/robots.txt`).

Within packet stream 5 (`seq 1001:1141`), a request targeting `/api/status` contains an explicit HTTP Basic Authentication header:

```http
GET /api/status HTTP/1.1
Host: intranet.corp
User-Agent: curl/8
Authorization: Basic c3ZjOkNURntjbDM0cnQzeHRfY3IzZHNfMG5fdGgzX3cxcjN9
```

## 3. Demodulation & Flag Extraction

Decoding the base64-encoded credential payload:

```bash
echo "c3ZjOkNURntjbDM0cnQzeHRfY3IzZHNfMG5fdGgzX3cxcjN9" | base64 -d
```

Output:
```text
svc:CTF{cl34rt3xt_cr3ds_0n_th3_w1r3}
```

## 4. Key Takeaways
- Unencrypted transport-layer communication (`HTTP` over port 80) exposes RFC 7617 Basic Authentication headers directly on the wire.
- In automated monitoring and daemon environments, credential exposure via unencrypted network segments remains a trivial path for privilege compromise.
