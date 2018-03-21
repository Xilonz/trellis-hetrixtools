# Trellis HetrixTools PHP Agent

[![Ansible Role](https://img.shields.io/ansible/role/20311.svg)](https://galaxy.ansible.com/TypistTech/trellis-hetrixtools-php/)
[![Build Status](https://travis-ci.org/TypistTech/trellis-hetrixtools-php.svg?branch=master)](https://travis-ci.org/TypistTech/trellis-hetrixtools-php)
[![GitHub tag](https://img.shields.io/github/tag/TypistTech/trellis-hetrixtools-php.svg)](https://github.com/TypistTech/trellis-hetrixtools-php/tags)
[![license](https://img.shields.io/github/license/TypistTech/trellis-hetrixtools-php.svg)](https://github.com/TypistTech/trellis-hetrixtools-php/blob/master/LICENSE)
[![Donate](https://img.shields.io/badge/Help-Donate-blue.svg)](https://typist.tech/donation/)
[![Hire Steenbergen Design](https://img.shields.io/badge/Hire-Typist%20Tech-ff69b4.svg)](https://typist.tech/contact/)

Install [HetrixTools PHP agent](https://docs.hetrixtools.com/docs/agents/php-agent) on [Trellis](https://github.com/roots/trellis) servers

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Requirements](#requirements)
- [Installation](#installation)
- [Role Variables](#role-variables)
- [Hacking Trellis' Playbook](#hacking-trellis-playbook)
- [Common Errors](#common-errors)
  - [`vault_hetrixtools_license` is not defined](#vault_hetrixtools_license-is-not-defined)
  - [HetrixTools merges multiple environments into single application](#new-relic-merges-multiple-environments-into-single-application)
  - [Error after upgrading PHP version](#error-after-upgrading-php-version)
- [Limitations](#limitations)
- [See Also](#see-also)
- [Support!](#support)
  - [Donate](#donate)
  - [Why don't you hire me?](#why-dont-you-hire-me)
  - [Want to help in other way? Want to be a sponsor?](#want-to-help-in-other-way-want-to-be-a-sponsor)
- [Feedback](#feedback)
- [Change log](#change-log)
- [Author Information](#author-information)
- [Contributing](#contributing)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Requirements

* [Ansible](http://docs.ansible.com/ansible/latest/intro_installation.html) 2.3 or later
* [Trellis](https://github.com/roots/trellis)
* [HetrixTools](https://hetrixtools.com/) account
* Ubuntu 16.04 (Xenial)

## Installation

Add this role to `requirements.yml`:

```yaml
- src: TypistTech.trellis-hetrixtools-php # Case-sensitive!
  version: 0.4.0 # Check for latest version!
```

Run `$ ansible-galaxy install -r requirements.yml` to install this new role.

## Role Variables

```yaml
# group_vars/<environment>/vault.yml
# This file should be encrypted. See: https://roots.io/trellis/docs/vault/
##########################################################################

# HetrixTools License Key
## See: https://docs.hetrixtools.com/docs/accounts-partnerships/accounts/account-setup/license-key
vault_hetrixtools_license: xxxxxxxxxxx

# group_vars/<environment>/main.yml
###################################

# Indicates the desired package state.
# `latest` ensures that the latest version is installed.
# `present` does not update if already installed.
# Choices: present|latest
# Default: latest
hetrixtools_package_state: present

# Check for default values here: https://github.com/TypistTech/trellis-hetrixtools-php/blob/master/defaults/main.yml
# See also: https://docs.hetrixtools.com/docs/agents/php-agent/configuration/php-agent-configuration
hetrixtools_config:
  appname: "My Awesome App {{ env }}"
  framework: no_framework
  transaction_tracer.detail: 1
  datastore_tracer.database_name_reporting.enabled: true
```

## Hacking Trellis' Playbook

Add this role to `dev.yml` and `server.yml` **immediately after** `role: php`:

```yaml
roles:
    # Some other Trellis roles ...
    - { role: php, tags: [php] }
    - { role: TypistTech.trellis-hetrixtools-php, tags: [php, hetrixtools-php] }
    # Some other Trellis roles ...
```

## Common Errors

### `vault_hetrixtools_license` is not defined

Encrypt your HetrixTools license key in `group_vars/<environment>/vault.yml`. See [role variables](#role-variables).

### HetrixTools merges multiple environments into single application

Solution: Define different `appname` for different environments.

Tips:
```yaml
# group_vars/all/main.yml
#########################

hetrixtools_config:
  appname: "My Awesome App {{ env }}"
```

### Error after upgrading PHP version

HetrixTools would fail and causes provision end up in errors when upgrading PHP minor releases (e.g: from 7.1 to 7.2).

After PHP minor release upgrade (i.e: when you see the error):
```
➜ ssh admin@123.456.789
➜ sudo hetrixtools-install install
➜ sudo reboot

# Wait for server reboot and re-provision again
➜ ansible-playbook server.yml -e env=production
```

## Limitations

* Only one HetrixTools APM application per server

Pull requests are welcomed.

## See Also

* [HetrixTools PHP agent docs](https://docs.hetrixtools.com/docs/agents/php-agent)
* [Ansible Vault](https://roots.io/trellis/docs/vault/)

## Support!

### Donate

Love Trellis HetrixTools PHP Agent? Help me maintain it, a [donation](https://typist.tech/donation/) can help with it.

### Why don't you hire me?

Ready to take freelance WordPress jobs. Contact me via the contact form [here](https://typist.tech/contact/) or, via email [info@typist.tech](mailto:info@typist.tech)

### Want to help in other way? Want to be a sponsor?

Contact: [Arjan Steenbergen](mailto:tangrufus@gmail.com)

## Feedback

**Please provide feedback!** We want to make this library useful in as many projects as possible.
Please submit an [issue](https://github.com/TypistTech/trellis-hetrixtools-php/issues/new) and point out what you do and don't like, or fork the project and make suggestions.
**No issue is too small.**

## Change log

Please see [CHANGELOG](./CHANGELOG.md) for more information on what has changed recently.

## Author Information

[Trellis HetrixTools PHP Agent](https://github.com/TypistTech/trellis-hetrixtools-php) is a [Steenbergen Design](https://typist.tech) project and maintained by [Arjan Steenbergen](https://twitter.com/Tangrufus), freelance developer for [hire](https://typist.tech/contact/).

Special thanks to [the Roots team](https://roots.io/about/) whose [Trellis](https://github.com/roots/trellis) make this project possible.

Full list of contributors can be found [here](https://github.com/TypistTech/trellis-hetrixtools-php/graphs/contributors).

## Contributing

Please see [CODE_OF_CONDUCT](./CODE_OF_CONDUCT.md) for details.

## License

[Trellis HetrixTools PHP Agent](https://github.com/TypistTech/trellis-hetrixtools-php) is released under the [MIT License](https://opensource.org/licenses/MIT).
