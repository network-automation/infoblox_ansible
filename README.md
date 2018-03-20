# Infoblox Ansible Examples

This repo contains various examples using Ansible for Infoblox Network Identity Operating System (NIOS).

# Table of Contents
  - [Ansible Module Examples](#ansible-module-examples)
    - [Configuring a IPv4 Network with nios_network](#configuring-a-ipv4-network-with-nios_network)
    - [Additional Examples](#additional-examples)
  - [Ansible Lookup Plugin Examples](#ansible-lookup-plugin-examples)
    - [Get a host record](#get-a-host-record)
    - [Get a network view object](#get-a-network-view-object)

## Ansible Module Examples

There are 5 modules that have been added to Ansible 2.5.  They can be currently seen in the devel branch of the documentation:
  - [nios_host_record](http://docs.ansible.com/ansible/devel/modules/nios_host_record_module.html) - for configuring host records
  - [nios_network](http://docs.ansible.com/ansible/devel/modules/nios_network_module.html) - for configuring networking objects
  - [nios_network_view](http://docs.ansible.com/ansible/devel/modules/nios_network_view_module.html) - for configuring networking views
  - [nios_dns_view](http://docs.ansible.com/ansible/devel/modules/nios_dns_view_module.html) - for configuring DNS views
  - [nios_zone](http://docs.ansible.com/ansible/devel/modules/nios_zone_module.html) - for configuring DNS zones

### Configuring an IPv4 Network with nios_network

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

The full playbook can be found here: [module_playbooks/configure_network.yml](module_playbooks/configure_network.yml)

### Additional Examples

There are 3 other playbooks in the **module_playbooks** directory that can be used as examples:
  - [module_playbooks/dns_instance.yml](module_playbooks/dns_instance.yml) - configure a dns zone on the system
  - [module_playbooks/dns_view.yml](module_playbooks/dns_view.yml) - configure a new dns view instance
  - [module_playbooks/host_record.yml](module_playbooks/host_record.yml) - configure an ipv4 host record

## Ansible Lookup Plugin Examples

The full documentation for the NIOS lookup plugin can be found here: [http://docs.ansible.com/ansible/devel/plugins/lookup/nios.html](http://docs.ansible.com/ansible/devel/plugins/lookup/nios.html)

### Get a host record

```
    - name: fetch host leaf01
      set_fact:
        host: "{{ lookup('nios', 'record:host', filter={'name': 'leaf01'}, provider=nios_provider) }}"

    - name: check the leaf01 return variable
      debug:
        var: host
```

The full playbook can be found here: [lookup_playbooks/get_host_record.yml](lookup_playbooks/get_host_record.yml)

### Get a network view object

```
    - name: fetch all networkview objects
      set_fact:
        networkviews: "{{ lookup('nios', 'networkview', provider=nios_provider) }}"

    - name: check the networkviews
      debug:
        var: networkviews
```

The full playbook can be found here: [lookup_playbooks/get_networkviews.yml](lookup_playbooks/get_networkviews.yml)

---
![Red Hat Ansible Automation](images/rh-ansible-automation.png)

Red Hat® Ansible® Automation includes three products:

- [Red Hat® Ansible® Engine](https://www.ansible.com/ansible-engine): a fully supported product built on the foundational capabilities of the Ansible project.

- [Red Hat® Ansible® Networking Add-On](https://www.ansible.com/ansible-engine): provides support for select networking modules from Arista (EOS), Cisco (IOS, IOS XR, NX-OS), Juniper (Junos OS), Open vSwitch, and VyOS.

- [Red Hat® Ansible® Tower](https://www.ansible.com/tower): makes it easy to scale automation, manage complex deployments and speed productivity. Extend the power of Ansible with workflows to streamline jobs and simple tools to share solutions with your team.

Want more info?
[Read this blog post for more info about Engine, the networking add-on and Tower](https://www.ansible.com/blog/red-hat-ansible-automation-engine-vs-tower)
