### Hardware

WordOps is very lightweight, and does not require much processing power

- ~30MB of free space
- 512MB RAM

### Operating Systems

The following operating systems are **officially** supported:

Distribution | Release            | Architecture
------------ | ------------------ | ------------
**Ubuntu**   | 16.04 LTS (xenial) | x86_64
             | 18.04 LTS (bionic) | x86_64
**Debian**   | 8 (jessie)         | x86_64
             | 9 (stretch)        | x86_64

### Ports

Service         | Port  | Inbound | Outbound | Notes
--------------- | ----- | ------- | -------- | --------------------------------------------------------------------
SSH             | 22    | ✓       | ✓        | You are free to use a custom port instead of the default 22
HTTP            | 80    | ✓       | ✓        | Nginx listen on port 80
HTTPS           | 443   | ✓       | ✓        | Nginx listen on port 443
WordOps Backend | 22222 | ✓       | ✓        | WordOps backend is available on port 22222 and is password protected
GnuPG           | 1137  |         | ✓        | Required to import APT repositories GPG keys.
