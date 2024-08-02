---
layout: post
title: Ansible - Structuring Inventory with Multiple Files and Formats
categories: ansible
tags: ansible
---

This guide outlines how to effectively organize an Ansible inventory using a combination of multiple files and formats, such as YAML and INI. It provides insights into creating a structured inventory system that enhances manageability and scalability of Ansible playbooks.

- [Ansible: Structuring Inventory with Multiple Files and Formats](#ansible-structuring-inventory-with-multiple-files-and-formats)
    - [For reference](#for-reference)
    - [Inventory structure](#inventory-structure)
    - [Utilizing Ansible Inventory Command](#utilizing-ansible-inventory-command)
    - [Executing Ansible Modules Across Inventory Groups](#executing-ansible-modules-across-inventory-groups)
    - [Conclusion](#conclusion)

```bash
$ ansible --version
ansible [core 2.17.0]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/Users/testing_user/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /Users/testing_user/.pyenv/versions/3.11.0/lib/python3.11/site-packages/ansible
  ansible collection location = /Users/testing_user/.ansible/collections:/usr/share/ansible/collections
  executable location = /Users/testing_user/.pyenv/versions/3.11.0/bin/ansible
  python version = 3.11.0 (main, Dec  4 2022, 11:20:26) [Clang 14.0.0 (clang-1400.0.29.202)] (/Users/testing_user/.pyenv/versions/3.11.0/bin/python3.11)
  jinja version = 3.1.4
  libyaml = True
```

## For reference

The official documentation outlines the process of organizing inventory within a directory

* https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html

```doc
Organizing inventory in a directory

You can consolidate multiple inventory sources in a single directory. 
The simplest version of this is a directory with multiple files instead of a single inventory file. 
A single file gets difficult to maintain when it gets too long. 
If you have multiple teams and multiple automation projects, having one inventory file per team or project lets everyone easily find the hosts and groups that matter to them.

You can also combine multiple inventory source types in an inventory directory. 
This can be useful for combining static and dynamic hosts and managing them as one inventory. 
```

Let's explore this concept further.

## Inventory structure

The inventory is organized into a directory named testing_multiple_files_inventory with subdirectories and files representing different environments or clusters.

```bash
$ tree testing_multiple_files_inventory 
testing_multiple_files_inventory
├── pg_cluster_b_db
│   ├── pg-cluster-01_02.yml
│   └── pg-cluster-03.yml
├── standalone.yml
└── vagrant
    └── cluster_a
        └── vagrant_cluster_a.yml

3 directories, 4 files

$ cat testing_multiple_files_inventory/standalone.yml
---
all:
  children:
    pg_standalone_a:
      hosts:
        standalone.example.com:
          ansible_host: 10.0.0.122

$ cat testing_multiple_files_inventory/pg_cluster_b_db/pg-cluster-01_02.yml 
---
all:
  children:
    pg_cluster_b:
      children:
        pg_cluster_b_db:
          hosts:
            pg-cluster-01.example.com:
              ansible_host: 10.0.0.123
            pg-cluster-02.example.com:
              ansible_host: 10.0.0.124

$ cat testing_multiple_files_inventory/pg_cluster_b_db/pg-cluster-03.yml   
---
all:
  children:
    pg_cluster_b:
      children:
        pg_cluster_b_db:
          hosts:
            pg-cluster-03.example.com:
              ansible_host: 10.0.0.125

$ cat testing_multiple_files_inventory/vagrant/cluster_a/vagrant_cluster_a.yml 
[vagrant]
vagrant1 ansible_ssh_host=127.0.0.1 ansible_ssh_port=2222
vagrant2 ansible_ssh_host=127.0.0.1 ansible_ssh_port=2200
vagrant3 ansible_ssh_host=127.0.0.1 ansible_ssh_port=2201
```

## Utilizing Ansible Inventory Command

Generate a visual representation of the inventory hierarchy, showing groupings and hosts:

```bash
$ ansible-inventory -i testing_multiple_files_inventory --graph
@all:
  |--@ungrouped:
  |--@pg_cluster_b:
  |  |--@pg_cluster_b_db:
  |  |  |--pg-cluster-01.example.com
  |  |  |--pg-cluster-02.example.com
  |  |  |--pg-cluster-03.example.com
  |--@pg_standalone_a:
  |  |--standalone.example.com
  |--@vagrant:
  |  |--vagrant1
  |  |--vagrant2
  |  |--vagrant3
```

## Executing Ansible Modules Across Inventory Groups

Test connectivity to specific hosts using ansible module ping

```bash
$ ansible all -i testing_multiple_files_inventory -m ping -l pg_cluster_b
pg-cluster-03.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.9"
    },
    "changed": false,
    "ping": "pong"
}
pg-cluster-02.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.9"
    },
    "changed": false,
    "ping": "pong"
}
pg-cluster-01.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.9"
    },
    "changed": false,
    "ping": "pong"
}
```

## Conclusion

Organizing Ansible inventory using multiple files and formats offers a flexible and scalable approach to managing complex environments. By structuring inventories thoughtfully, teams can enhance collaboration, simplify management tasks, and execute targeted operations efficiently across various groups of hosts.
