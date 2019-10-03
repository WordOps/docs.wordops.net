# LTS Enablement Stacks

The Ubuntu LTS enablement (also called HWE or Hardware Enablement) stacks provide newer kernel and X support for existing Ubuntu LTS releases.

## How to install HWE stacks on Ubuntu

To enable HWE stacks on Ubuntu 18.04 LTS, you just have to run the following command :

```bash
sudo apt-get install --install-recommends linux-generic-hwe-18.04 -y
```

After the install process, you will just have to reboot your server to boot on the new kernel :

```bash
sudo shutdown -r now
```
