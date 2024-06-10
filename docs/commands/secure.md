# Secure

Secure command secure WordOps backend auth, ip and port

<asciinema-player src="/images/wosecure.cast" autoplay loop cols="125" rows="30"></asciinema-player>

Usage:

```bash
wo secure [options]
```

Options:

| argument          | description                                                        |
| ----------------- | ------------------------------------------------------------------ |
| `--auth`          | Set backend user credentials (user and)                            |
| `--port`          | Set backend port (default: 22222)                                  |
| `--ip`            | Set the list of IP(s) allowed to access without authentification   |
| `--ssh`           | Harden SSH security                                                |
| `--sshport`       | Set custom ssh port (default: 22)                                  |
| `--allowpassword` | Allow password authentification when hardening SSH security        |
| `--force`         | Force hardening SSH security without being prompt for confirmation |

WordOps uses [Basic Auth](https://docs.nginx.com/nginx/admin-guide/security-controls/configuring-http-basic-authentication/) to protect the backend from unauthorize people. To change the authorization method, backend's port,... You can use `wo secure` command.

## Change backend credential

The user name and password of WordOps backend is showed when you create a first site. If you don't remember and want to reset, please use below command.

```bash
wo secure --auth
Provide HTTP authentication user name [admin]:master
Provide HTTP authentication password [5zVFELjHjShPPFr7qkoMzavP]:
```

Short hand:

```bash
wo secure --auth YourUsername aSecurePassword
```

## Change backend port

In case you want to change WordOps backend port from `22222`, use this command:

```bash
wo secure --port
WordOps admin port [22222]:23456
Reload: nginx     [OK]
Successfully port changed 23456
```

## Change whitelist IPs

[By default](https://github.com/WordOps/WordOps/blob/master/wo/cli/templates/acl.mustache), WordOps only allow IP `127.0.0.1` to connect to their backend. To allow your IP (ex. `1.1.1.1`), use below command:

```bash
wo secure --ip
Enter the comma separated IP addresses to white list [127.0.0.1]:1.1.1.1
Successfully added IP address in acl.conf file
```

You can also edit directly the file `/etc/nginx/common/acl.conf`

## Harden SSH security

<!-- prettier-ignore -->
!!! warning

    To harden SSH security, WordOps render the configuration sshd_config from a template. In this template, root authentification with password is forbidden and by default password authentification is disabled. You can use the flag `--allowpassword` with `--ssh` to allow password authentification, but before running this command please make sure you will not be locked out of your server. Using password-less authentification with SSH keys is highly recommended.

<!-- prettier-ignore-end -->

To harden SSH security you can use the command :

```bash
wo secure --ssh
```

Additionally, if you want to allow password authentification (not recommended), you can use :

```bash
wo secure --ssh --allowpassword
```

## Change SSH port

To avoid bruteforce on SSH, it's recommended to use another port than the default port (22).

Usage :

```bash
wo secure --sshport <port>
```

Exemple :

```bash
wo secure --sshport 2022
```

WordOps will automatically allow the new SSH port if UFW is enabled.
