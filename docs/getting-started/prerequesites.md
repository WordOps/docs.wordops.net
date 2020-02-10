# Prerequesites

## Hardware requirements

### Resources

#### Minimum

WordOps is very lightweight, it doesn't require a lot of resources and can be installed on low end devices like Raspberry PI. Minimum requirements are:

- ~100MB of storage
- 512MB RAM

#### Recommended

However, if you are going to use WordOps in production, some services like MySQL or Redis may need more resources, and running WordOps stacks without enough resources could impact your sites performance. Resources usage also highly depend on your site traffic.

Here our recommended hardware configuration for production:

- Multi-core CPU
- 20GB SSD storage
- 2GB RAM

### Virtualization

The following virtualization platforms are supported:

- VMware
- XEN
- OpenVZ
- KVM
- Hyper-V
- LXC / LXD

WordOps is also compatible with Ubuntu running on Windows Linux Subsystem (WSL).

## Software requirements

### Operating Systems

The following operating systems are supported:

| Distribution | Release            | Architecture |
| ------------ | ------------------ | ------------ |
| **Ubuntu**   | 18.04 LTS (bionic) | x86_64       |
|              | 16.04 LTS (xenial) | x86_64       |
| **Debian**   | 9 (stretch)        | x86_64       |
|              | 10 (buster)        | x86_64       |
| **Raspbian** | 9 (stretch)        | armv7l       |
|              | 10 (buster)        | armv7l       |

### Ports

| Service         | Port  | Inbound | Outbound | Notes                                                                |
| --------------- | ----- | ------- | -------- | -------------------------------------------------------------------- |
| SSH             | 22    | ✓       | ✓        | SSH default or custom port                                           |
| HTTP            | 80    | ✓       | ✓        | Nginx listen on port 80                                              |
| HTTPS           | 443   | ✓       | ✓        | Nginx listen on port 443                                             |
| WordOps Backend | 22222 | ✓       | ✓        | WordOps backend is available on port 22222 and is password protected |
| GnuPG           | 1137  |         | ✓        | Required to import APT repositories GPG keys.                        |

## Server configuration recommendations

- Set a valid server hostname (see below)

??? Info "Proper server hostname configuration"
    Server hostname isn't only a name, it's the server public identity on the network. If your server is directly connected to internet(not behind a NAT),
    it should have a valid hostname.

    A **valid hostname** should looks like : myservername.yourdomain.tld

    - myservername is the server name
    - yourdomain.tld is one of your domains

    To edit hostname properly, use the command :

    ```bash
    hostnamectl set-hostname <yourserver.hostname.tld>
    ```

    To apply the new hostname, a reboot is required.
    The last step and the most important, you should create the proper DNS records to make the subdomain myservername.yourdomain.tld pointing to your server IP.
