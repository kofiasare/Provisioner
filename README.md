# Ansible Rails app deploy

Server provisioning for rails app.

## Description

Rails application deploy server provisioning for staging and production environment.

### Prerequisites

Require Ansible in local machine.
For ansible installation check here: [Ansible installation](http://docs.ansible.com/ansible/latest/intro_installation.html#installation).

### Configuration
Need few step of configuration for server provision.
#### hosts
hosts file will be contain host server credentials and how ansible will be connect with server from local machine.

Do same same step for [production_server] and [staging_server] block:

1. In 'hosts' file set server ip
2. Set ansible_ssh_user: server login user name
3. Set ansible_ssh_private_key_file: server login ssh private key

Example:
```
<Server Ip> ansible_ssh_user=<Server login User> ansible_ssh_private_key_file=<server ssh private key path>
```

```
[production_server]
192.168.33.10 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

[staging_server]
192.168.33.10 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
```

## Usage

## Contributing
Bug reports and pull requests are welcome on GitHub at [Ansible Rails App Server Provision](https://github.com/tanvir002700/Ansible-Rails-App-Server-Provision).
This project is intended to be a safe, welcoming space for collaboration,
and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## Authors
* **Tanvir Hasan** - *Owner* - [Tanvir002700](https://github.com/tanvir002700)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details