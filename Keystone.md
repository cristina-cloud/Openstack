# Installing Keystone #

#### Keystone is an Identity service that provides a single point of intergration for managing authentication, authorization, and a catalog of services by implementing Openstack's Identity API. ####

#####Before you install and configure the Identity service, you must create a database.#####

1. Creating a database
```
$ mysql -u root -p -> Use the database access client to connect to the database server as the root user

MariaDB [(none)]> CREATE DATABASE keystone; -> Create the keystone database

MariaDB [(none)]> GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'localhost' \ 
IDENTIFIED BY 'KEYSTONE_DBPASS';
MariaDB [(none)]> GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'%' \
IDENTIFIED BY 'KEYSTONE_DBPASS';
-> Grant proper access to the keystone database
```

2. Install and configure components
```

```
