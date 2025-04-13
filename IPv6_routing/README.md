IPv6_Routing
=========

This role will render a basic EIGRPv6 config and static routes onto a Cisco IOS-XE router via NETCONF. This role was tested against a Cisco Catalyst 8000v router w/IOS-XE v17.15

Requirements
------------

ncclient is required to use the Ansible netconf_config module called in this role. Target router must have NETCONF enabled, use router command "netconf-yang".

Role Variables
--------------

This role leverages Jinja2 templates to build the NETCONF payload. The expected variables come from Ansible host vars and are structured like this:

eigrp_v6:
  as: #autonomous system number
  interfaces:
    - name:  #gigabitethernet interface number, e.g. "1" or "0/1"
  router_id: #String, dotted decimal router id e.g. 1.1.1.1

default_route: # variables for static routes.
  name: "default"
  identifier:
    - type: "STATIC"
      name: "static"
  destination: "::/0" #identifies any IPv6 destination prefix
  next_hop: #String. next-hop router, does not support outbound interface w/link-local address as next hop

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
    - IPv6_routing


License
-------

BSD

Author Information
------------------

Made at the University of Arizona
