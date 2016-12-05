stunnel
=======

Role which helps to install and configure Stunnel.

The configuration of the role is done in such way that it should not be necessary
to change the role for any kind of configuration. All can be done either by
changing role parameters or by declaring completely new configuration as a
variable. That makes this role absolutely universal. See the examples below for
more details.

Please report any issues or send PR.


Example
-------

```
---

- name: Example of how to configure Stunnel
  hosts: host1
    # This is the configuration
    stunnel_config:
      smtps:
        accept: 5000
        client: "yes"
        connect: outbound.att.net:465
  roles:
    - stunnel
```


Role variables
--------------

List of variables used by the role:

```
# Package to be installed (explicit version can be specified here)
stunnel_pkg: stunnel

# Name of the Stunnel service
stunnel_service: stunnel

# Whether to install the service file
stunnel_service_install: yes

# Path of the init.d script
stunnel_service_upstart: /etc/init.d/{{ stunnel_service }}

# Path of the systemd script
stunnel_service_systemd: /usr/lib/systemd/system/{{ stunnel_service }}.service

# Data structure which helps to choose the right service script
stunnel_service_script:
  systemd:
    src: stunnel.systemd
    dest: "{{ stunnel_service_systemd }}"
  upstart:
    src: stunnel.upstart
    dest: "{{ stunnel_service_upstart }}"
    mode: "0755"

# Location of the Stunnel config file
stunnel_config_file: /etc/stunnel/stunnel.conf

# Stunnel configuration
stunnel_config: {}
```


Dependencies
------------

- [`config_encoder_filters`](https://github.com/jtyr/ansible-config_encoder_filters)


License
-------

MIT


Author
------

Jiri Tyr
