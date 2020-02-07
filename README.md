# Veryfy Backend API Server-Provision ( Ansbile )

Server provisioning for veryfy api.

## Description

Rails application deploy server provisioning for staging and production environment.

### Prerequisites

Require Ansible in local machine.
For ansible installation check here: [Ansible installation](http://docs.ansible.com/ansible/latest/intro_installation.html#installation).

### Configuration

Need few step of configuration for server provision.

#### - hosts

hosts file will contain host server credentials and how ansible will connect with server from local machine.

Do same same step for [production] and [staging] block:

1. In 'hosts/production' or 'hosts/staging' file set server ip
2. Set ansible_ssh_user: server login user name
3. Set ansible_ssh_private_key_file: server login ssh private key

Example:

```
<Server Ip> ansible_ssh_user=<Server login User> ansible_ssh_private_key_file=<server ssh private key path>
```

```
#hosts/production
[production]
192.168.33.10 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

#hosts/staging
[staging]
192.168.33.10 ansible_ssh_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
```

#### - common configuration

In this section all changes will be in 'group_var/all' file.

1. Set Deploy user name to 'deploy_user' variable
   ```
       deploy_user: <deploy_user>
   ```
   Example:
   ```
      deploy_user: deploy
   ```
2. Set App name to 'app_name' variable
   ```
       app_name: <application_name>
   ```
   Example:
   ```
      app_name: demo_app
   ```
3. Set ruby version to 'ruby_version' variable

   ```
       ruby_version: <ruby_version>
   ```

   Example:

   ```
      ruby_version: 2.4.0
   ```

#### - Staging and production separate configuration

In this section all changes will in 'group_var/production/' and 'group_var/staging/' files.

1. If using postgres database then add postgres user name and password to 'postgres_user' and 'postgres_password both file.
   Example:

   ```
       #group_var/production/database.yml
       postgres_user: applicationProduction
       postgres_password: appPassword
   ```

   ```
       #group_var/staging/database.yml
        postgres_user: applicationProduction
        postgres_password: appPassword
   ```

#### - Configure GitHub access key

- Put GitHub access public and private key in the 'roles/create-deploy-user/templates' path And adding '.j2' extension to them.
  ```
      id_rsa.j2       #put into 'roles/create-deploy-user/templates' path.
      id_rsa.put.j2   #put into 'roles/create-deploy-user/templates' path.
  ```

## Usage

For start server provisioning first clone the repo, and from root run following command:

```
    $ansible-playbook setup-provision.yml -i hosts/production -e app_env=production    #for production server
    $ansible-playbook setup-provision.yml -i hosts/staging -e app_env=staging          #for staging server
```

Run ansible playbook with sudo password:

```
    $ansible-playbook setup-provision.yml -i hosts/production -e app_env=production --extra-vars "ansible_sudo_pass=<password>"
    $ansible-playbook setup-provision.yml -i hosts/staging -e app_env=staging  --extra-vars "ansible_sudo_pass=<password>"
```

## Contributing

Bug reports and pull requests are welcome on GitHub at [Ansible Rails App Server Provision](https://github.com/tanvir002700/Ansible-Rails-App-Server-Provision).
This project is intended to be a safe, welcoming space for collaboration,
and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## Authors

- **Tanvir Hasan** - _Owner_ - [Tanvir002700](https://github.com/tanvir002700)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

1. Copy public key of your computer to the server to be provisioned such that you can login
   ssh-copy-id root@<server-to-be-provisioned>

2. Enter the CI server switch to the go user `su go` and copy public key of CI server to the server to be provisioned such that you can login from the CI server to the provision servre

ssh-copy-id root@<server-to-be-provisioned>

NB: when prompted for password, use root password set on linode for server under provisioning

3. Run apt update and upgrade on the provision server.

4. Run ansible provision playbook

5.
