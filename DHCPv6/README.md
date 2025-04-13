DHCPv6
=========

This role will configure DHCPv6 for IPv6 on a Cisco IOS-XE router via NETCONF. This role was tested against a Cisco Catalyst 8000v router w/IOS-XE v17.15

Requirements
------------

ncclient is required to use the Ansible netconf_config module called in this role. Target router must have NETCONF enabled, use router command "netconf-yang".

Role Variables
--------------

This role leverages Jinja2 templates to build the NETCONF payload. The expected variables come from Ansible host vars and are structured like this:

dhcpv6:
  pool_name: "v6_pool"
  subnet:
    ip_address: "2001:db8:10::/64"
    prefix_length: 64
  lease:
    duration: 3600
  interfaces: "2"
  dns: "2001:4860:4860::8888"


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
    - DHCPv6


License
-------

BSD

Author Information
------------------

Made at the University of Arizona
