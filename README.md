# ansible-debian-tor

ansible-debian-tor is an Ansible playbook to bootstrap a debian 9 server to be used as tor node. It performs some basic configuration
and basic hardening (first n minutes on an new server like) on the server and it installs and configures a tor node with tor monitoring tools
[nyx](https://nyx.torproject.org/) and [theonionbox](https://github.com/ralphwetzel/theonionbox).

It's based on light forks of some great roles around, used as git submodules:

* [ansible-role-unattended-upgrades](https://github.com/jnv/ansible-role-unattended-upgrades)
* [geerlingguy nginx](https://github.com/geerlingguy/ansible-role-nginx)
* [geerlingguy certbot](https://github.com/geerlingguy/ansible-role-certbot)
* [ansible-relayor](https://github.com/nusenu/ansible-relayor)

It configures by distinct roles:

* basic users
* ssh
* basic packages
* motd
* fail2ban
* mail for notifications
* unattended updates by unattended upgrades
* certbot to obtain a ssl certificate for the nginx serving the onionbox
* nginx to proxy theonionbox webapps
* tor to install and configure tor
* tor-mon to install and configure nyx and theonionbox

## Install
### Clone
```bash
git clone https://github.com/lgaggini/ansible-debian-tor.git
git submodule init
git submodule update
```
## Configuration

The configuration is done by the [group_vars/all](https://github.com/lgaggini/ansible-debian-tor/blob/master/group_vars/all.yml) file.
Options are self-explanatory. 
Passwords can be setted by using Ansible Vault.

## Usage

```bash
ansible-playbook -i hosts playbook.yml --tags {{ tag }}
```

Available tags are:

* user
* ssh
* packages
* motd
* fail2ban
* mail
* unattended-upgrades
* certbot
* nginx
* tor
* tor-mon

## On air
[nibiru.lgaggini.net](https://nibiru.lgaggini.net)
