# Trellis HetrixTools Agent

Install [HetrixTools agent](https://docs.hetrixtools.com/category/server-monitor/) on [Trellis](https://github.com/roots/trellis) servers


## Requirements

* [Ansible](http://docs.ansible.com/ansible/latest/intro_installation.html) 2.3 or later
* [Trellis](https://github.com/roots/trellis)
* [HetrixTools](https://hetrixtools.com/) account
* Ubuntu 16.04 (Xenial)

## Role Variables

```yaml
# group_vars/<environment>/main.yml
###################################

hetrixtools_config:
  services: "nginx,mysql,php,fail2ban,ferm,cron,ntp,ssh"

```

## Hacking Trellis' Playbook

Add this role to `server.yml` **after** the last role:

```yaml
roles:
    # All other Trellis roles ...
    - { role: wordpress-setup, tags: [wordpress, wordpress-setup, letsencrypt] }
    - { role: trellis-hetrixtools, tags: [hetrixtools-php], when: sites_using_hetrixtools | count}
```

## Limitations

* Only one HetrixTools Agent per server

Pull requests are welcomed.

## See Also

* [HetrixTools PHP agent docs](https://docs.hetrixtools.com/category/server-monitor/)

## Author Information

[Trellis HetrixTools PHP Agent](https://github.com/Xilonz/trellis-hetrixtools) is a [Steenbergen Design](https://steenbergen.design) project and maintained by Arjan Steenbergen

Special thanks to [the Roots team](https://roots.io/about/) whose [Trellis](https://github.com/roots/trellis) make this project possible, and [TypistTech](https://github.com/TypistTech/) for the [inspiration](https://github.com/TypistTech/trellis-newrelic-php/).

Full list of contributors can be found [here](https://github.com/Xilonz/trellis-hetrixtools/graphs/contributors).

## Contributing

Please see [CODE_OF_CONDUCT](./CODE_OF_CONDUCT.md) for details.

## License

[Trellis HetrixTools Agent](https://github.com/Xilonz/trellis-hetrixtools) is released under the [MIT License](https://opensource.org/licenses/MIT).
