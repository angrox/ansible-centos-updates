# Centos-Updates

This module has the following features:
* Apply Updates
** Security only
** Complete
* Reboot the maschine if necessary
* Activate automatic installation of security relevant updates (each day) without reboot


## Usage
The module needs variables set to work properly. When using ansible-playbook you can provide them with the option "-e". 

### Apply Updates & Reboot
```
ansible-playbook site.yml -e 'security_updates=true'
ansible-playbook site.yml -e 'update_all=true'
```
If necessary the server can be rebooted. 

```
ansible-playbook site.yml -e 'do_reboot=true'
ansible-playbook site.yml -e 'update_all=true do_reboot=true'
```

### Automatic Updates
This is done by installing yum-cron and activate the yum-cron system service

```
ansible-playbook site.yml -e 'automatic_updates=true'
```

=== Do everything
```
ansible-playbook site.yml -e 'update_all=true do_reboot=true automatic_updates=true'
```

== Defaults
By default nothing is done except a message is print that a task needs to be specified

One variable can be defined: What should be included in the autmatic updates: 
```
#  What kind of update to use:
# default                            = yum upgrade
# security                           = yum --security upgrade
# security-severity:Critical         = yum --sec-severity=Critical upgrade
# minimal                            = yum --bugfix update-minimal
# minimal-security                   = yum --security update-minimal
# minimal-security-severity:Critical =  --sec-severity=Critical update-minimal
yum_update_command: minimal-security
```


