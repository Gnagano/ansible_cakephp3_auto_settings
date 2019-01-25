# Ansible Role: cakephp3 application auto settings

When you install cakephp3 application for development, you need to do below.

- composer update
- edit app.php
- database migration
- edit config file for web server application (ex. nginx)

This process should be automated and this role is for the automation.

## Requirements

- OS: Ubuntu16.04
- php version is higher than 7.0
- database server is MySql

## Setup

```
$ ansible_galaxy install Gnagano.ansible_cakephp3_project_setup --roles-path <your_roles_directory>
```

## Usage

Copy `defaults/main.yml.default` as `defaults/main.yml` and edit `main.yml`. The roles variables on main.yml are depends on you. Please read the next section `Role Varibles` below.
After editing main.yml, just execute main.yml

## Role Variables (you need to edit)

#### cakephp3_project_name

  The name of what you want to create app

#### cakephp3_app_dir

  The directory where your new app is installed.

#### php_fpm_version

  Set version of php_fpm, default value is `7.0`.
  
#### cakephp3_nginx_conf_dir

  The directory path for nginx conf file.
  The default value is `/etc/nginx/sites-enabled/`.
  
#### cakephp3_nginx_default_conf

  The file path for nginx conf file.
  The default value is `/etc/nginx/sites-enabled/default`.

#### cakephp3_nginx_server_name

  The server name set on nginx conf file.
  Additionaly, the routing will be added on `/etc/hosts` as `127.0.0.1 {{ cakephp3_nginx_server_name }}`

#### cakephp3_nginx_service_port

  The port used by nginx, default value is `80`.

#### cakephp3_default_env_name
#### cakephp3_test_env_name

  The name of CAKE_ENV. 
  The role will be create `{{ cakephp3_nginx_conf_dir }}/{{ cakephp3_nginx_default_env_name }}` and `{{ cakephp3_nginx_conf_dir }}/{{ cakephp3_nginx_test_env_name }}` as new nginx conf file as the copy of default conf file.
  The default values are `development` as `{{ cakephp3_default_env_name }}`, `test` as `{{ cakephp3_test_env_name }}`

#### cakephp3_security_salt

  Plese set your app's security_salt which will be added in app.php

#### mysql_user
#### mysql_host
#### mysql_password
#### mysql_database

  Those valiables are for database settings written on `config/app.php`
  As the name of variable, they will be set , host, username, password and database name.

#### mysql_test_user
#### mysql_test_host
#### mysql_test_password
#### mysql_test_database

  Those variables are for test database.

#### cakephp3_email_host
#### cakephp3_email_port
#### cakephp3_email_address
#### cakephp3_email_password

  Those valiables are for email settings.
  As the name of variable, they will be set hostname, port, address, password.
