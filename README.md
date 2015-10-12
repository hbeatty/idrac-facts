# idrac-facts
Ansible role that works with the [iDRAC Ansible module](https://github.com/hbeatty/iDRAC-Ansible-module).

## Tasks - tasks/main.yml

* Get System Inventory (ignore_errors)
* Reset Default Password (if Get System Inventory Failed)
* Get Firmware Info

## Variables - defaults/main.yml

* lom_user: root
* lom_pass: pass
* drac_default_pass: calvin

## Handlers - handlers/main.yml

* Get System Inventory

## Dependencies

* [iDRAC Ansible module](https://github.com/hbeatty/iDRAC-Ansible-module)
* [Dell WSMan Client API Python](https://github.com/hbeatty/dell-wsman-client-api-python)
* wsmancli and libwsman1 from [OpenWSMAN](https://openwsman.github.io/)
  * I would like to get rid of this dependency (for various reasons) by enhancing the Dell WSMan Client API Python with a new transport.

## Example Playbook

```

- hosts: localhost
  sudo: yes
  tasks:
  - name: Install wsmancli
    yum: name=wsmancli state=present


- hosts: idracs
  gather_facts: False
  sudo: yes

  roles:
    - idrac-facts
    - idrac-firmware
    - idrac-storage
    - idrac-iso
```
