# Rails-App-Server-Provision ( Ansbile )

Server provisioning for rails app.

## Description

Rails application deploy server provisioning for staging and production environment.

### Prerequisites

Require Ansible in local machine.
For ansible installation check here: [Ansible installation](http://docs.ansible.com/ansible/latest/intro_installation.html#installation).

### Configuration
Need few step of configuration for server provision.
#### - hosts
hosts file will be contain host server credentials and how ansible will be connect with server from local machine.

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
In this section all changes will in 'group_var/all' file.

1. Add server remote user name to 'remote_user' variable
    ```
        remote_user: <server_remote_user>
     ```
     Example:
     ```
        remote_user: ubuntu
     ```
2. Set Deploy user name to 'deploy_user' variable
    ```
        deploy_user: <deploy_user>
     ```
     Example:
     ```
        deploy_user: deployer
     ```
3. Set App name to 'app_name' variable
    ```
        app_name: <application_name>
     ```
     Example:
     ```
        app_name: demo_app
     ```
4. Set ruby and node version to 'ruby_version' & 'node_version' variable
    ```
        ruby_version: <ruby_version>
        node_version: <node_version>
     ```
     Example:
     ```
        ruby_version: 2.4.0
        node_version: 7.7.4
     ```
5. if Want to use mysql db then Set 'mysql_setup' value true, Otherwise set it is false. And set mysql port and root user password.
     Example:
     ```
        mysql_setup: true
        mysql_port: 3306
        mysql_root_password: <root_password>
     ```
6. If want to use postgres db the Set 'postgres_setup' value true, Otherwise set it is false.
     Example:
     ```
         postgres_setup: false
     ```
#### - Staging and production separate configuration
In this section all changes will in 'group_var/production/' and 'group_var/staging/' files.

1. If using mysql database then add mysql_user name and password to 'mysql_user' and 'mysql_user_password
     both file.
    Example:
    ```
        #group_var/production/database.yml
        mysql_user: applicationProduction
        mysql_user_password: appPassword
    ```

    ```
        #group_var/staging/database.yml
        mysql_user: applicationStaging
        mysql_user_password: appPassword
    ```

2. If using postgres database then add postgres user name and password to 'postgres_user' and 'postgres_password both file.
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
* Put GitHub access public and private key in the 'roles/create-deploy-user/templates' path And adding '.j2' extension to them.
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
* **Tanvir Hasan** - *Owner* - [Tanvir002700](https://github.com/tanvir002700)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details