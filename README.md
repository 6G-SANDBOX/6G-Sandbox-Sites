<a name="readme-top"></a>

# 6G-Sandbox-Sites <!-- omit in toc -->

Repository with unique information for each 6G-SANDBOX site. It use composed of different yaml files with different variables usable by the [6G-Library](https://github.com/6G-SANDBOX/6G-Library) components.


<details>
<summary>Table of Contents</summary>

- [Site Directory Structure](#site-directory-structure)
- [How to encrypt your site files](#how-to-encrypt-your-site-files)
  - [1. Install ansible-core](#1-install-ansible-core)
  - [2. Set a password to encrypt/decrypt](#2-set-a-password-to-encryptdecrypt)
  - [3. Encrypt your site file](#3-encrypt-your-site-file)
- [Development Guidelines](#development-guidelines)

</details>

## Site Directory Structure

```
site_name/       # Directory with the site name
└── core.yaml    # File containing the encrypted site information
```

The repository is made up of yaml variable files divided into different directories representing each site. The purpose of having a different directory per site is in case future releases allow importing more than one file per site (apart from `core.yaml`).

The [`.dummy_site/core.yaml`](.dummy_site/core.yaml) file serves as a template of the information that can/should be indicated for each site.

The files belonging to each site are encrypted with a passphrase using the [Ansible vault](https://docs.ansible.com/ansible/latest/vault_guide/index.html) utility.

## How to encrypt your site files

This section aims to serve as a guide on how to fill your site's `core.yaml` file.

#### 1. Install ansible-core

To use the `ansible-vault` tool, the full *ansible* libraries and binaries are not needed. You can [install ansible](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html) in your prefered way, but package `ansible-core` is enough.
If you do not wish to install *ansible* anywhere, remember it is already installed on the Jenkins VM so you can use it from there.

#### 2. Set a password to encrypt/decrypt

Your password should be a random string of characters stored in a file.

> [!CAUTION]
> Try to avoid scapable special characters as ", ', `, ´, #, $, &,...
> 
> Unpredictable errors might happen.

> [!TIP]
> Typical recommendations are:
>
> - String size: >=20
> - Uppercase letters (A-Z)
> - Lower case letters (a-z)
> - Numbers (0-9)
> - Special characters (excluding scapable special characters)
>
> You can use any [online password generator](https://www.random.org/strings/) to create it.

#### 3. Encrypt your site file

```sh
ansible-vault encrypt <site_name>/core.yaml --vault-password-file=path/to/password.txt
```

where:

- `<site_name>/core.yaml` is the path to the file you want to encrypt.
- `--vault-password-file=path/file_name.txt` is the path containing the password.

Running this command will **replace** the original contents of the file with the encrypted text.

With the same syntaxt, you can use other `ansible-vault` commands to edit your encrypted file:
- `ansible-vault edit`; Opens the file to correct its unencrypted content.
- `ansible-vault decrypt`; Decrypts the content of the file, replacing the encrypted text with the unencrypted one.

# Development guidelines
Despite the main branch having a directory for all known sites, we are aware that development might involve a lot of minor commits that can blur the repo for other developers.

Thus, the recommended way of using this repository is to fork it or to make your own branch with your site directory, where you can do as many commits as you want.

<p align="right"><a href="#readme-top">Back to top&#x1F53C;</a></p>