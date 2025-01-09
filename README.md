<a name="readme-top"></a>

# 6G-Sandbox-Sites <!-- omit in toc -->

Repository with unique information for each 6G-SANDBOX site. It is composed of different yaml files with different variables usable by the [6G-Library](https://github.com/6G-SANDBOX/6G-Library) components, encrypted via `ansible-vault`.
> [!TIP]
> Your site name should be a simple string made of lowercase characters and numbers


<details>
<summary>Table of Contents</summary>

- [Site Directory Structure](#site-directory-structure)
- [Development guidelines](#development-guidelines)
- [How to encrypt your site file](#how-to-encrypt-your-site-file)

</details>

## Site Directory Structure

```
site_name/       # Directory with the site name
└── core.yaml    # File containing the encrypted site information
```

The repository is made up of yaml variable files divided into different directories representing each site. The purpose of having a different directory per site is in case future releases allow importing more than one file per site (apart from `core.yaml`).

The [`.dummy_site/core.yaml`](.dummy_site/core.yaml) file serves as a template of the information that can/should be indicated for each site.

The files belonging to each site are encrypted with a passphrase using the [Ansible vault](https://docs.ansible.com/ansible/latest/vault_guide/index.html) utility.

## Development guidelines

The recommended way of using this repository is to fork it or to make your own branch with your site directory.

## How to encrypt your site file

This section aims to serve as a guide on how to fill your site's `core.yaml` file.

### 1. Install ansible-core <!-- omit in toc -->

To use the `ansible-vault` tool, the full *ansible* libraries and binaries are not needed. You can [install ansible](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html) in your prefered way, but package `ansible-core` is enough.
If you do not wish to install *ansible* anywhere, remember it is already installed on the Jenkins VM so you can use it from there.

```bash
apt install ansible-core
```

### 2. Set a password to encrypt/decrypt <!-- omit in toc -->

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

### 3. Encrypt your site file <!-- omit in toc -->

```sh
ansible-vault encrypt <site_name>/core.yaml --vault-password-file=path/to/password.txt
```

where:

- `<site_name>/core.yaml` is the path to the file you want to encrypt.
- `--vault-password-file=path/file_name.txt` is the path containing the password.

Running this command will **replace** the original contents of the file with the encrypted text.

With the same syntaxt, you can use other `ansible-vault` commands to edit your encrypted file:
- `ansible-vault edit`: open the file to correct its unencrypted content.
- `ansible-vault decrypt`: decrypt the content of the file, replacing the encrypted text with the unencrypted one.

<p align="right"><a href="#readme-top">Back to top&#x1F53C;</a></p>
