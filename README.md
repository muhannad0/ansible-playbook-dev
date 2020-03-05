# Ansible Playbooks (dev)
This repo is meant for playbooks I usually write for testing out stuff.

They are stable but ...

***_DISCLAIMER:_** These playbooks are NOT meant for production use.*

## Features
* [Initial OS Setup](#initial-setup)
* [LAMP Stack Setup](#lamp-stack)
* [Deploy a Website](#deploy-a-website)
* [Docker Host Setup (dev)](#Docker-Host-Setup-(Dev))

## Supported OS
* Ubuntu Server 18.04 LTS

Currently only Ubuntu is supported. But I plan on adding support for CentOS as well.

## Usage

I recommend to start out with a fresh image.

### Define your hosts and variables

#### Hosts File
Add your hosts to `hosts.example` with the necessary tags

Rename it to `hosts`.

#### Variables File
Change the values in `vars.yml.example` with the necessary info

Rename it to `vars.yml`.

### Initial Setup

Run playbook `init.yml` to setup the users and update the OS.

Give the initial user/pass if needed. You can also define it in the playbook `ansible_user` variable.

```
ansible-playbook -i hosts init.yml -u root --ask-pass
```

### LAMP Stack
Run playbook `lamp-stack.yml` to setup Apache, MySQL and PHP.

```
ansible-playbook -i hosts lamp-stack.yml
```

#### PHP Versions
Depending on your requirement, edit the playbook to import the tasks for the PHP version.

* PHP 5.6
```
- import_tasks: tasks/php56-tasks.yml
```
* PHP 7.4
```
- import_tasks: tasks/php74-tasks.yml
```

### Deploy a Website
Run playbook `deploy-site-sample.yml` to deploy a website.

This playbook configures the directories, sets up database, configures virtual host and copies a sample index page. You should modify it to your requirements.

#### Define the variables required for the website.
* domain_name
* mysql_app_db
* mysql_app_user
* mysql_app_user_pass

```
ansible-playbook -i hosts deploy-site-example.yml
```

### Docker Host Setup (Dev)
Run playbook `docker-stack.yml` to setup Docker and Docker Compose
```
ansible-playbook -i hosts docker-stack.yml
```
Note: The plan is to use these playbooks to spin up a containerized app stack.

## Feedback
Feel free to provide any suggestions/improvements.

## Acknowledgements
* [Ansible for DevOps](https://leanpub.com/ansible-for-devops) book by [Jeff Geerling](https://github.com/geerlingguy/)
* [DigitalOcean Ansible Tutorials](https://www.digitalocean.com/community/tags/ansible)