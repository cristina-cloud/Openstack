# Prerequisite before installing Openstack #

###### * This is Stein version but it's better to use the recent version to avoid dependency and any other errors in the future * ######
###### * Software Version : CentOS Linux release 7.3.1611 (Core) ######

## What to do?

1. yum install centos-release-openstack-stein.noarch -y (repository)
2. yum repo list 
3. yum upgrade
4. SQL database setting 
```
# yum install mariadb mariadb-server python2-PyMySQL 
# systemctl enable mariadb.service
# systemctl start mariadb.service 
```
5. Message queue setting
```
# yum install rabbitmq-server
# systemctl enable rabbitmq-server.service
# systemctl start rabbitmq-server.service
# rabbitmqctl add_user openstack RABBIT_PASS 
(rabbitmqctl add_user [username] [password] You can set any password for user Openstack)
# rabbitmqctl set_permissions openstack ".*" ".*" ".*" (Granting all permissions to the user)
```
6. Memcached setting
```
# yum install memcached python-memcached
# vi /etc/sysconfig/Memcached 
# systemctl enable memcached.service
# systemctl start memcached.service
```




##### *I basically referenced the webiste, docs.openstack.org, to create the Openstack tutorials #####

