Monarx Agent Role
=========

Ansible role to configure and install [Monarx](https://www.monarx.com/) Agent and Monarx cPanel/WHM Plugins (where applicable).

Tested on:
- AlmaLinux 9 / Rocky Linux 9 / CloudLinux 9
- CentOS 8 / AlmaLinux 8 / Rocky Linux 8 / CloudLinux 8
- CentOS 7 / CloudLinux 7
- Ubuntu 23 (Lunar Lobster)
- Ubuntu 22 (Jammy Jellyfish)
- Ubuntu 20 (Focal Fossa)
- Ubuntu 18 (Bionic Beaver)
- Ubuntu 16 (Xenial Xerus)
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Debian 12 (Bookworm)

Requirements
------------

None

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

```
client_id: "CLIENTID" # Required - Monarx API Client ID
client_secret: "SECRET" # Required - Monarx API Client Secret
```
The `client_id` and `client_secret` variables are required to register the Monarx Agent with the [administration dashboard](https://app.monarx.com)

The following variables are optional and can be used to customize the agent, if not provided, the default values are used:
```
user_bases: # Optional - Base Directory(-ies) for Users
  - /home/
  - /var/www/
exclude_dirs: # Optional - Excluded directories
  - /virtfs
  - /(clam_|\.)?quarantine
  - ^/home/quarantine/
exclude_users: # Optional - Excluded users
  - ^virtfs$
advanced_options: # Optional - Advanced Options
  - { name: "quarantine.global", value: "/var/log/.quarantine/" }
  - { name: "quarantine.user", value: "$USER/.quarantine/ $USER $USER 0700" }
agent_tags: # Optional - Agent Tafs
  - tag1
  - tag2
```

The following variables indicate whether you want to install the cPanel and WHM Plugins. if set to `true`, the playbook would check if cPanel is installed before attempting to install the plugins:
```
install_cpanel_plugin: true # Optional - Install cPanel Plugin
install_whm_plugin: true # Optional - Install WHM Plugin
```

Dependencies
------------

None

Example Playbook
----------------

```
- hosts: servers
  roles:
     - { role: libyanspider.monarx_agent, client_id: "MYCLIENTID", client_secret: "MYSECRET", agent_tags: [upsell, vps] }
```

License
-------

BSD

Author Information
------------------

Ahmed Shibani (#shumbashi) sheipani@gmail.com.
