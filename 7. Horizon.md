# Installing Horizon(Dashboard) #

### Horizon is the canonical implementation of Openstack's Dashboard, which provides a web based user interface to Openstack services including Nova, Swift, Keystone, etc ###

1. Installing and configuring components
```
# yum install openstack-dashboard

vi /etc/openstack-dashboard/local_settings 

OPENSTACK_HOST = "controller"
#OPENSTACK_HOST = "127.0.0.1"
OPENSTACK_KEYSTONE_URL = "http://%s:5000/v3" % OPENSTACK_HOST
#OPENSTACK_KEYSTONE_DEFAULT_ROLE = "user"
OPENSTACK_KEYSTONE_DEFAULT_ROLE = "member"
#OPENSTACK_KEYSTONE_DEFAULT_ROLE = "_member_"

ALLOWED_HOSTS = ['*']

CACHES = {
    'default': {
         'BACKEND': 'django.core.cache.backends.memcached.MemcachedCache',
         'LOCATION': 'controller:11211',
    }
}

# If you use ``tox -e runserver`` for developments,then configure
# SESSION_ENGINE to django.contrib.sessions.backends.signed_cookies
# as shown below:
#SESSION_ENGINE = 'django.contrib.sessions.backends.signed_cookies'
SESSION_ENGINE = 'django.contrib.sessions.backends.cache'

OPENSTACK_KEYSTONE_URL = "http://%s:5000/v3" % OPENSTACK_HOST

OPENSTACK_API_VERSIONS = {
    "identity": 3,
    "image": 2,
    "volume": 3,
}

OPENSTACK_KEYSTONE_DEFAULT_DOMAIN = 'Default'

# The OPENSTACK_NEUTRON_NETWORK settings can be used to enable optional
# services provided by neutron. Options currently available are load
# balancer service, security groups, quotas, VPN service.
OPENSTACK_NEUTRON_NETWORK = {
    'enable_router': True,
    'enable_quotas': True,
    'enable_ipv6': True,
    'enable_distributed_router': False,
    'enable_ha_router': False,
    'enable_fip_topology_check': True,
    
# The timezone of the server. This should correspond with the timezone
# of your entire OpenStack installation, and hopefully be in UTC.
TIME_ZONE = "Asia/Seoul"
#TIME_ZONE = "UTC"


vi /etc/httpd/conf.d/openstack-dashboard.conf
WSGIDaemonProcess dashboard
WSGIProcessGroup dashboard
WSGISocketPrefix run/wsgi
WSGIApplicationGroup %{GLOBAL}

WSGIScriptAlias /dashboard /usr/share/openstack-dashboard/openstack_dashboard/wsgi/django.wsgi
Alias /dashboard/static /usr/share/openstack-dashboard/static

<Directory /usr/share/openstack-dashboard/openstack_dashboard/wsgi>
  Options All
  AllowOverride All
  Require all granted
</Directory>

<Directory /usr/share/openstack-dashboard/static>
  Options All
  AllowOverride All
  Require all granted
</Directory>
```

2. finalize installation
```
# systemctl restart httpd.service memcached.service 
```

3. Verify operation

1. Access the dashboard using a web browser at http://controller/dashboard.

2. Authenticate using admin or demo user and default domain credentials.
