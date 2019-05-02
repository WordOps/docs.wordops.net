# Prerequesites

## Hardware requirements

### Minimum

WordOps is very lightweight, it doesn't require a lot of resources and can be installed on low end devices like Raspberry PI. Minimum requirements are :

- ~100MB of storage
- 512MB RAM

### Recommended

However, if you are going to use WordOps in production, some services like MySQL or Redis may need more resources, and running WordOps stacks without
enough resources could impact your sites performance. Resources usage also highly depend on your site traffic.
Here our recommended hardware configuration for production :

- Multi-core CPU
- 20GB SSD storage
- 2GB RAM

## Operating Systems

The following operating systems are supported:

Distribution | Release            | Architecture
------------ | ------------------ | ------------
**Ubuntu**   | 16.04 LTS (xenial) | x86_64
             | 18.04 LTS (bionic) | x86_64
             | 19.04 (disco)      | x86_64
**Debian**   | 8 (jessie)         | x86_64
             | 9 (stretch)        | x86_64
**Raspbian** | 9 (stretch)        | armv7l

## Ports

Service         | Port  | Inbound | Outbound | Notes
--------------- | ----- | ------- | -------- | --------------------------------------------------------------------
SSH             | 22    | ✓       | ✓        | You are free to use a custom port instead of the default 22
HTTP            | 80    | ✓       | ✓        | Nginx listen on port 80
HTTPS           | 443   | ✓       | ✓        | Nginx listen on port 443
WordOps Backend | 22222 | ✓       | ✓        | WordOps backend is available on port 22222 and is password protected
GnuPG           | 1137  |         | ✓        | Required to import APT repositories GPG keys.
