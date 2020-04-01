# How to automate WordOps installation

During WordOps installation, you will be prompted for a username and an email (required for git configuration). But it's pretty easy to make WordOps installation non-interactive.

## Method 1 : using the `--force` flag

To allow users to perform non-interactive installation of WordOps, we added the flag `--force` into our install script.

This way you just have to use the following command to install WordOps without being prompted :

```bash
wget -qO wo wops.cc && sudo bash wo --force
```

## Method 2 : using the .gitconfig file

If you prefer to configure manually git before installing WordOps, this can be done by creating a .gitconfig file in your user home directory.

You can use the command `git config --global --edit` to create this file and edit it with your preferred text editor.

It should look like the following example :

```gitconfig
[user]
       name = user
       email = user@domain.tld
```
