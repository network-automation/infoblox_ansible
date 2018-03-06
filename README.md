# Infoblox Ansible Examples

This repo contains various examples using Ansible for Infoblox Network Identity Operating System (NIOS).

# Table of Contents
  - [Ansible Module Examples](Ansible_Module_Examples)
  - [Configuring a IPv4 Network with nios_network](Configuring_a_IPv4_Network_with_nios_network)

## Ansible Module Examples

### Configuring a IPv4 Network with nios_network

```yaml
    - name: set dhcp options for a network
      nios_network:
        network: 192.168.100.0/24
        comment: sean put a comment here
        options:
          - name: domain-name
            value: ansible.com
        state: present
        provider: "{{nios_provider}}"
```

The full playbook can be found here: [module_playbooks/configure_network.yml](configure_network.yml)

### Additional Examples

There are 3 other playbooks in the **module_playbooks** directory that can be used as examples:
  - [module_playbooks/dns_instance.yml](dns_instance.yml) - configure a dns zone on the system
  - [module_playbooks/dns_view.yml](dns_view.yml) - configure a new dns view instance
  - [module_playbooks/host_record.yml](host_record.yml) - configure an ipv4 host record

## Ansible Lookup Plugin Examples

## Get a host record

```
    - name: fetch host leaf01
      set_fact:
        host: "{{ lookup('nios', 'record:host', filter={'name': 'leaf01'}, provider=nios_provider) }}"

    - name: check the leaf01 return variable
      debug:
        var: host
```

The full playbook can be found here: [lookup_playbooks/get_host_record.yml](get_host_record.yml)

## Get a network view object

```
    - name: fetch all networkview objects
      set_fact:
        networkviews: "{{ lookup('nios', 'networkview', provider=nios_provider) }}"

    - name: check the networkviews
      debug:
        var: networkviews
```

The full playbook can be found here: [lookup_playbooks/get_networkviews.yml](get_networkviews.yml)

---
![Red Hat Ansible Automation](images/rh-ansible-automation.png)

Red Hat® Ansible® Automation includes three products:

- [Red Hat® Ansible® Engine](https://www.ansible.com/ansible-engine): a fully supported product built on the foundational capabilities of the Ansible project.

- [Red Hat® Ansible® Networking Add-On](https://www.ansible.com/ansible-engine): provides support for select networking modules from Arista (EOS), Cisco (IOS, IOS XR, NX-OS), Juniper (Junos OS), Open vSwitch, and VyOS.

- [Red Hat® Ansible® Tower](https://www.ansible.com/tower): makes it easy to scale automation, manage complex deployments and speed productivity. Extend the power of Ansible with workflows to streamline jobs and simple tools to share solutions with your team.

Want more info?
[Read this blog post for more info about Engine, the networking add-on and Tower](https://www.ansible.com/blog/red-hat-ansible-automation-engine-vs-tower)
