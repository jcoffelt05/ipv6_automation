# ipv6_automation
Proof of concept for using Ansible to automate IPv6 adoption

Internet Protocol version 6 (IPv6) was introduced in 1998 as a replacement for the legacy IPv4 protocol, which continues to address most internet-connected devices. While IPv6 offers significant improvements, such as an exponential increase in available addresses, its adoption has been slow due to concerns about effort required and the potential for network disruptions. Despite this, the need for IPv6 adoption is growing as IPv4 address exhaustion worsens and the demand for internet connected devices grows, posing challenges for organizations that rely on legacy addressing schemes. Advancements in network automation and new concepts such as Infrastructure as Code (IaC) have introduced modern approaches that simplify network configuration and reduce manual effort. Existing bodies of evidence show that these new concepts are achieving wide adoption, primarily in IPv4 environments. This project seeks to prove that modern network configuration methods and tools can expedite IPv6 adoption in an existing IPv4 based network. To demonstrate these concepts in an IPv6 context, an IPv4 based network was created using Cisco Modeling Labs. An IPv6 design was then developed to work in conjunction with the legacy design, often referred to as the dual-stack method, and translated into a set of variables to for consumption by Ansible using Jinaj2 templates. The automation process then successfully applied IPv6 configurations across the network without disrupting the existing IPv4 infrastructure. This outcome highlights that using modern approaches to configure networks can significantly reduce the barriers to IPv6 adoption. As IPv6 adoption continues to grow, these modern approaches offer a practical solution for organizations seeking to remain relevant with the greater internet community.

# Lab Design
![image](https://github.com/user-attachments/assets/2268b222-a23f-4623-bb92-d14eefcba5d5)

This lab uses Ansible's NETCONF_CONFIG module to configure the target Cisco Routers. This is achieved by rendering host variables onto jinja2 templates to then be applied to the target device as a NETCONF payload. This lab uses both OpenConfig and native Cisco IOS-XE YANG models to structure the NETCONF templates. This lab is designed to be used at a home or small office that offers native IPv6 connectivity to the virtual environment, however these playbooks can easily be extended to support configuring NAT64. The clients and routers below the WAN router are addressed using the IPv6 Documentation Prefix which is then translated to Global Unicast address space at WAN Router's GigabitEthernet1 interface. If you cannot support the use of NETCONF please review the provided templates and playbooks and update the use the provided Network_CLI versions of each role.

# Before first use
- Check and update host variables to match your virtual environment

# Requirements
-Ansible
-Cisco Modeling Labs Personal (paid version required to support NETCONF)
-NCClient
