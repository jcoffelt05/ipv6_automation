IPv6 Prefix Translation
=========

This role will render NPTv6 config onto a Cisco IOS-XE router via NETCONF. This role was tested against a Cisco Catalyst 8000v router w/IOS-XE v17.15

Requirements
------------

ncclient is required to use the Ansible netconf_config module called in this role. Target router must have NETCONF enabled, use router command "netconf-yang".

Role Variables
--------------

This role leverages Jinja2 templates to build the NETCONF payload. The expected variables come from Ansible host vars and are structured like this:

nat66:
 inside_interface: "2" #gigabitethernet interface number
 outside_interface: "1" #gigabitethernet interface number
 prefix:
   inside: #String. Inside prefix
   outside: #string, outside prefix

Dependencies
------------

None

Example Playbook
----------------

- name: IPv6 Migration - Configure IPv6 Interfaces and Routing on Routers
  hosts: routers
  connection: netconf
  gather_facts: false
  roles:
    - IPv6_prefix_translation


License
-------

BSD

Author Information
------------------

Made at the University of Arizona
