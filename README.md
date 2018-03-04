Ansible Role: ProxySQL
=========

[![Build Status](https://travis-ci.org/kenanfallon/ansible-role-proxysql.svg?branch=master)](https://travis-ci.org/kenanfallon/ansible-role-proxysql)
[![Ansible Galaxy](https://img.shields.io/ansible/role/23915.svg)](https://galaxy.ansible.com/kenanfallon/proxysql/)

Installs & configures ProxySQL on Ubuntu servers

Requirements
------------

None.

Role Variables
--------------

```yaml
# Basic settings
proxysql_admin_user: admin
proxysql_admin_password: admin
proxysql_admin_interface: 0.0.0.0
proxysql_admin_port: 6032

# ProxySQL Users
proxysql_mysql_users:
   - username: username
     password: password
     default-hostgroup: 1 #default 1
     active: 1 #default 1
   - username: username1
     password: password1
     default-hostgroup: 2 #default 1
     active: 1 #default 1

# ProxySQL Servers
proxysql_mysql_servers:
   - address: 127.0.0.1
     port: 3306
     hostgroup: 1 # default 1 
   - address: 127.0.0.1
     port: 3307
     hostgroup: 2 # default 1 
     status: OFFLINE_SOFT #default ONLINE
     weight: 2 # default 1

# ProxySQL Replication Hostgroups
proxysql_mysql_replication_hostgroups:
  - writer_hostgroup: 1
    reader_hostgroup: 2
    comment: default
     
# ProxySQL Query Rules        
proxysql_mysql_query_rules:
    - match_digest: '^SELECT (.*) FOR UPDATE$'
      destination_hostgroup: 2
      username: username
      apply: 1
   - match_pattern: "^SELECT"
     destination_hostgroup: 2 
     username: username
     apply: 1
   - digest: '0x2XXXXXXXXXXXXXXX'
     destination_hostgroup: 2
     username: username
     apply: 1   
```

For all available variables, take a look at defaults/main.yml

Dependencies
------------

None.

Example Playbook
------------

    - hosts: localhost
      vars:
        proxysql_admin_user: admin
        proxysql_admin_password: admin
        proxysql_mysql_servers:
            - address: 127.0.0.1
              port: 3306
              hostgroup: 1
      roles:
        - kenanfallon.proxysql

License
-------

MIT / BSD

Author Information
------------------

This role was created in 2018 by Kenan Fallon.