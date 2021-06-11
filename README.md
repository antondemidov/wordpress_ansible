# Wordpress on Ubuntu 20.04 LAMP

This playbook will install a WordPress website on top of a LAMP environment (**L**inux, **A**pache, **M**ySQL and **P**HP) on an Ubuntu 20.04 machine.
Please note - playbook could install multiple wordpress websites to your host. Just adjust http_envs variable

## Settings

- `mysql_root_password`: The desired password for the **root** MySQL account.
- `mysql_password`: The password for the new MySQL user.
- `http_port`: HTTP port for this virtual host, where `80` is the default. 
- `http_envs`: if you need to install multiple instances of wordpress.
- `domain`: your domain.

## Running this Playbook

Quickstart guide for those already familiar with Ansible:

### 1. Customize Options

```
vim vars/main.yml
---
#System Settings
php_modules: [ 'php-curl', 'php-gd', 'php-mbstring', 'php-xml', 'php-xmlrpc', 'php-soap', 'php-intl', 'php-zip' ]

#MySQL Settings
mysql_root_password: "mysql_root_password"
mysql_password: "password"

#HTTP Settings
http_port: "80"
http_envs: ['woocommerce-dev', 'woocommerce-qa']
```

### 2. Run the Playbook

```command
ansible-playbook -l [target] -i [inventory file] -u [remote user] playbook.yml
```

### 3. Obtain Let's Encrypt Certificates
```
certbot --apache -d woocommerce-dev.example.com
certbot --apache -d woocommerce-qa.example.com
```

### 4. Proceed with the wordpress setup
