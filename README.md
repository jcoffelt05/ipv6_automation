# ipv6_automation
Proof of concept for using Ansible to automate IPv6 adoption

Internet Protocol version 6 (IPv6) was introduced in 1998 as a replacement for the legacy IPv4 protocol, which continues to address most internet-connected devices. While IPv6 offers significant improvements, such as an exponential increase in available addresses (Deering & Hindent, 2017), its adoption has been slow due to concerns about effort required and the potential for network disruptions (Pickard, Angolia, & Drummond, 2019). Despite this, the need for IPv6 adoption is growing as IPv4 address exhaustion worsens and the demand for internet connected devices grows, posing challenges for organizations that rely on legacy addressing schemes. Advancements in network automation and new concepts such as Infrastructure as Code (IaC) have introduced modern approaches that simplify network configuration and reduce manual effort. Existing bodies of evidence show that these new concepts are achieving wide adoption (Datta et al, 2023), primarily in IPv4 environments. This project seeks to prove that modern network configuration methods and tools can expedite IPv6 adoption in an existing IPv4 based network. To demonstrate these concepts in an IPv6 context, an IPv4 based network was created using Cisco Modeling Labs. An IPv6 design was then developed to work in conjunction with the legacy design, often referred to as the dual-stack method, and translated into a set of variables to for consumption by Ansible using Jinaj2 templates. The automation process then successfully applied IPv6 configurations across the network without disrupting the existing IPv4 infrastructure. This outcome highlights that using modern approaches to configure networks can significantly reduce the barriers to IPv6 adoption. As IPv6 adoption continues to grow, these modern approaches offer a practical solution for organizations seeking to remain relevant with the greater internet community.

# Lab Design
![image](https://github.com/user-attachments/assets/2268b222-a23f-4623-bb92-d14eefcba5d5)

This lab uses Ansible's NETCONF_CONFIG module to configure the target Cisco Routers. This is achieved by rendering host variables onto jinja2 templates to then be applied to the target device as a NETCONF payload. This lab uses both OpenConfig and native Cisco IOS-XE YANG models to structure the NETCONF templates. This lab is designed to be used at a home or small office that offers native IPv6 connectivity to the virtual environment, however these playbooks can easily be extended to support configuring NAT64. The clients and routers below the WAN router are addressed using the IPv6 Documentation Prefix which is then translated to Global Unicast address space at WAN Router's GigabitEthernet1 interface. If you cannot support the use of NETCONF please review the provided templates and playbooks and update to use the provided Network_CLI versions of each role.

# Before first use
- Check and update host variables to match your virtual environment

# Running the playbook
- The playbook titled "ipv6_migration.yml" is the primary task and calls all of the included roles.
- The playbook titled "ipv6_verification.yml" pulls the target routers interface configs and routing table entries so that the user can verify the changes took.

# Requirements
- Linux or Windows client w/Ansible
- Bridged connection between virtual environemnt (the CML lab) and local area network to allow Ansible client reachability
- Cisco Modeling Labs Personal (paid version required to support NETCONF)
- NCClient to allow Linux client to leverave NETCONF_CONFIG module

# References

- Datta, A. Imran, A., Biswas, C. (2023). Network Automation: Enhancing Operational Efficiency across the Network Environment. ICRRD Journal, 2023, 4(1), 101-111. 	https://doi.org/10.53272/icrrd.v4i1.1
- Deering, S., Hinden, R. (2017, July). Internet Protocol, Version 6 (IPv6) Specification. Internet Engineering Task Force (IETF). https://datatracker.ietf.org/doc/html/rfc8200.
- Pickard, J., Angolia, M., & Drummond, D. (2019). IPv6 Diffusion Milestones: Assessing the Quantity and Quality of Adoption. Journal of International Technology	and Information Management, 28(1), 2-27. https://scholarworks.lib.csusb.edu/jitim/vol28/iss1/1

# Related Documentation

- Ansible NETCONF_CONFIG: https://docs.ansible.com/ansible/latest/collections/ansible/netcommon/netconf_config_module.html
- Cisco Modeling Labs: https://www.cisco.com/site/us/en/learn/training-certifications/training/modeling-labs/resources.html
- Cisco YANG Models: https://github.com/YangModels/yang/tree/main/vendor/cisco/xe/1751
- Cisco YANG Suite: https://developer.cisco.com/yangsuite/
- Sempahore: https://semaphoreui.com/
