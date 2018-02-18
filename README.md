Ansible Role: ProxySQL
=========

Installs & configures ProxySQL on Debian/Ubuntu servers

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

# Proxy SQL Users
proxysql_mysql_users:
   - username: username
     password: password
     default-hostgroup: 1 #default 1
     active: 1 #default 1
   - username: username1
     password: password1
     default-hostgroup: 2 #default 1
     active: 1 #default 1

#Proxy SQL Servers
proxysql_mysql_servers:
   - address: 127.0.0.1
     port: 3306
     hostgroup: 1 # default 1 
      
proxysql_mysql_query_rules:
   - match_pattern: "^SELECT .* FOR UPDATE$"
     destination_hostgroup: 1
   - match_pattern: "^SELECT"
     destination_hostgroup: 2  
```

For all available variables, take a look at defaults/main.yml

Dependencies
------------

None.

License
-------

MIT / BSD

Author Information
------------------

This role was created in 2018 by Kenan Fallon.