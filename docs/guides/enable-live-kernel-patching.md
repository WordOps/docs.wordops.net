# Enable live kernel patching on Ubuntu

On linux servers, kernel updates usually require a reboot to apply the last security patches.
But there are several live kernel patching solutions available and in this short guide we will see how to enable Canonical Livepatch to apply critical kernel security fixes on your Ubuntu LTS server without rebooting.

## Requirements

Canonical Livepatch service is available on Ubuntu 14.04 LTS, 16.04 LTS, and 18.04 LTS.
This service is free for up to 3 machines (server, desktop or cloud).

## Setup

1. Get your Livepatch token on https://auth.livepatch.canonical.com/

2. Install the Livepatch daemon : `sudo snap install canonical-livepatch`

3. Enable Canonical Livepatch with your token : `sudo canonical-livepatch enable [TOKEN]`