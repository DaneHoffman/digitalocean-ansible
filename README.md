# DigitalOcean Ansible Playbooks

Requirements:

* A Digitalocean droplet
* Ansible installed on your local computer
* Basic knowledge of how Ansible works

## What does it do? 

This is a collection of Ansible playbooks for provisioning a DigitalOcean droplet. Playbooks used: 

* vps-init.yml: _Configures basic security for vps_
	
	1. creates `ansible` user (default for all future playbooks)
	2. sets ssh key for `ansible` user
	3. sets longer password for `root` user
	4. disables root login over ssh
	5. disables password authentication for ssh (keyfiles only)

* vps-users.yml: _Configures users, permissions, groups, authorized keys_
	
	1. creates admin user
	2. sets ssh key for admin user

* vps-packages.yml: _Installs and upgrades apt packages_
	
	1. Installs `aptitude` on server (preferred package manager for Ansible)
	2. Upgrades all packages
	3. Installs apt packages from list
	4. Autoremoves unused packages

* vps-docker.yml: _Installs docker and related modules_
	
	1. Add Docker GPG key
	2. Add Docker repository
	3. Installs `docker-ce` and `docker-compose`
	4. Installs `docker` pip module


Intended for use with the [Wordpress Docker-compose Template](https://github.com/DaneHoffman/wp-docker-template). Though it can be used to provision any basic dockerized hosting environment. 

## Why is it important?

Updating configurations using Ansible playbooks prevents configuration drift for clustered servers and automates the deployment of new nodes.

## How do I use it? 

1. Clone this repository
2. Fill in `vars/vars.yml` to set server IP addresses, user credentials
3. Edit packages and tasks as needed in `playbooks/`
4. Run `ansible ./playbooks/main.yml` to automatically configure new servers or update the configuration of existing ones


### Best practices: 
* Encrypt vars.yml with ansible-vault! 
* Add vars.yml to .gitignore