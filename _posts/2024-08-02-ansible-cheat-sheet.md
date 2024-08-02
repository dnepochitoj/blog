---
layout: post
title: Ansible - Cheat sheet
categories: ansible
tags: ansible
---

This Ansible cheat sheet gives you quick tips and reminders for the key commands, modules, and features in Ansible. Whether you're organizing your inventory, writing playbooks, securing secrets with Ansible Vault, or running one-off commands, this cheat sheet is handy, keeping important Ansible stuff easy to find.

All commands were run in a real setup. Every command is pretty much self-explanatory, with descriptions added only where necessary.

- [ansible cheat sheet](#ansible-cheat-sheet)
    - [ansible-doc](#ansible-doc)
        - [List modules](#list-modules)
        - [Describe module](#describe-module)
        - [Briefly describe module](#briefly-describe-module)
    - [ansible-inventory](#ansible-inventory)
        - [List the inventory in list form](#list-the-inventory-in-list-form)
        - [List the inventory as graph](#list-the-inventory-as-graph)
    - [ansible ad hoc commands](#ansible-ad-hoc-commands)
        - [Collect list of target hosts without executing any actions](#collect-list-of-target-hosts-without-executing-any-actions)
        - [Execute module against specific host](#execute-module-against-specific-host)
        - [Set verbosity level for debugging](#set-verbosity-level-for-debugging)
        - [Collect ansible facts about specific host](#collect-ansible-facts-about-specific-host)
        - [Execute shell command with source the environment](#execute-shell-command-with-source-the-environment)
        - [Execute command without source the environment](#execute-command-without-source-the-environment)
        - [Use pipe with shell commands](#use-pipe-with-shell-commands)
        - [Pipe failed with the `command` module](#pipe-failed-with-the-command-module)
        - [Transfer file from local host to remote host](#transfer-file-from-local-host-to-remote-host)
        - [Transfer file from remote host to local host](#transfer-file-from-remote-host-to-local-host)
        - [Delete file if it exists](#delete-file-if-it-exists)
        - [Download file from URL to local directory](#download-file-from-url-to-local-directory)
        - [Check the accessibility of website](#check-the-accessibility-of-website)
        - [Execute module with administrative privileges](#execute-module-with-administrative-privileges)
    - [ansible-vault](#ansible-vault)
        - [Create new encrypted file](#create-new-encrypted-file)
        - [View encrypted file](#view-encrypted-file)
        - [Edit encrypted file](#edit-encrypted-file)
        - [Change encryption key of encrypted file](#change-encryption-key-of-encrypted-file)
        - [Encrypt playbook file](#encrypt-playbook-file)
        - [Execute encrypted playbook file](#execute-encrypted-playbook-file)
        - [Decrypt playbook file](#decrypt-playbook-file)
        - [Encrypt string](#encrypt-string)
    - [ansible-playbook](#ansible-playbook)
        - [Check syntax of playbook](#check-syntax-of-playbook)
        - [List hosts, tags, and tasks defined in playbook](#list-hosts-tags-and-tasks-defined-in-playbook)
        - [Perform dry run of playbook, no actual changes](#perform-dry-run-of-playbook-no-actual-changes)
        - [Execute playbook on specific group of hosts](#execute-playbook-on-specific-group-of-hosts)
        - [Run playbook but only execute tasks tagged with 'my\_tag'](#run-playbook-but-only-execute-tasks-tagged-with-my_tag)
        - [Start executing playbook at specific task](#start-executing-playbook-at-specific-task)
        - [Execute playbook steps by step](#execute-playbook-steps-by-step)
        - [Execute playbook](#execute-playbook)
    - [ansible usefull modules](#ansible-usefull-modules)
        - [Module ping](#module-ping)
        - [Module setup](#module-setup)
        - [Module apt](#module-apt)
        - [Module yum](#module-yum)
        - [Module package](#module-package)
        - [Module pip](#module-pip)
        - [Module raw](#module-raw)
        - [Module command](#module-command)
        - [Module shell](#module-shell)
        - [Module script](#module-script)
        - [Module copy](#module-copy)
        - [Module fetch](#module-fetch)
        - [Module get\_url](#module-get_url)
        - [Module archive](#module-archive)
        - [Module unarchive](#module-unarchive)
        - [Module file](#module-file)
        - [Module template](#module-template)
        - [Module find](#module-find)
        - [Module replace](#module-replace)
        - [Module lineinfile](#module-lineinfile)
        - [Module blockinfile](#module-blockinfile)
        - [Module cron](#module-cron)
        - [Module debug](#module-debug)

## ansible-doc

The `ansible-doc` command provides documentation for Ansible modules, plugins, and other components. It allows users to quickly access information about available modules, their parameters, and usage examples, making it easier to understand and utilize the vast array of tools within Ansible.

### List modules

`ansible-doc -l`

`ansible-doc -l | egrep "postgresql\."`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
community.postgresql.postgresql_copy                     Copy data between a file/progr...
community.postgresql.postgresql_db                       Add or remove PostgreSQL dat...
community.postgresql.postgresql_ext                      Add or remove PostgreSQL e...
community.postgresql.postgresql_idx                      Create or drop indexes f...
community.postgresql.postgresql_info                     Gather information...
community.postgresql.postgresql_lang                     Adds, removes or changes procedural languages w...
community.postgresql.postgresql_membership               Add or remove Pos...
community.postgresql.postgresql_owner                    Change an owner of P...
community.postgresql.postgresql_pg_hba                   Add, remove or modif...
community.postgresql.postgresql_ping                     Check remote Postg...
community.postgresql.postgresql_privs                    Grant or revoke privileges on Po...
community.postgresql.postgresql_publication              Add, update, or remo...
community.postgresql.postgresql_query                    ...
community.postgresql.postgresql_schema                   Add or...
community.postgresql.postgresql_script                   Run PostgreS...
community.postgresql.postgresql_sequence                 Create, drop, or al...
community.postgresql.postgresql_set                      Change a PostgreSQL serve...
community.postgresql.postgresql_slot                     Add or remove replication slots f...
community.postgresql.postgresql_subscription             Add, update, or remov...
community.postgresql.postgresql_table                    Create, drop, or ...
community.postgresql.postgresql_tablespace               Add or remove PostgreSQL tabl...
community.postgresql.postgresql_user                     Create, alter, or remove a user (role) from a P...
community.postgresql.postgresql_user_obj_stat_info       Gather statistics abou...
```

</details>

### Describe module

`ansible-doc ping`

<details>
  <summary>Example Output (Click to expand)</summary>

```json

> MODULE ping (~/.pyenv/versions/3.11.0/lib/python3.11/site-packages/ansible/modules/ping.py)

A trivial test module, this module always returns `pong' on successful contact. It does not
make sense in playbooks, but it is useful from `/usr/bin/ansible' to verify the
ability to login and that a usable Python is configured.
This is NOT ICMP ping, this is just a trivial test module that requires Python on the
remote-node.
For Windows targets, use the ansible.windows.win_ping module instead.
For Network targets, use the ansible.netcommon.net_ping module instead.

OPTIONS (red indicates it is required):

data    Data to return for the `ping' return value.
        If this parameter is set to `crash', the module will cause an exception.
        default: pong
        type: str

ATTRIBUTES:

        check_mode:
        description: Can run in check_mode and return changed status prediction without modifying
        target, if not supported the action will be skipped.
        support: full

        diff_mode:
        description: Will return details on what has changed (or possibly needs changing in
        check_mode), when in diff mode
        support: none

        platform:
        description: Target OS/families that can be operated against
        platforms: posix
        support: N/A

SEE ALSO:
    * Module ansible.netcommon.net_ping
    * Module ansible.windows.win_ping

AUTHOR: Ansible Core Team, Michael DeHaan

EXAMPLES:
# Test we can logon to 'webservers' and execute python with json lib.
# ansible webservers -m ping

- name: Example from an Ansible Playbook
ping:

- name: Induce an exception to see what happens
ping:
    data: crash

RETURN VALUES:

ping    Value provided with the `data' parameter.
        returned: success
        sample: pong
        type: str

```

</details>

### Briefly describe module

`ansible-doc -s ping`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
- name: Try to connect to host, verify a usable python and return `pong' on success
  ping:
      data:                  # Data to return for the `ping' return value. If this parameter is set to `crash', the module will cause an exception.
```

</details>

## ansible-inventory

`ansible-inventory` is a command-line tool used to manage and visualize the inventory of hosts in Ansible. It enables users to list or export the inventory, showing groups, hosts, and variables associated with them. This tool is crucial for understanding the structure of your environment and ensuring that playbooks target the correct hosts.

### List the inventory in list form

`ansible-inventory -i testing_inventory.yml --list`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
{
    "_meta": {
        "hostvars": {
            "pg-cluster-01.example.com": {
                "ansible_host": "10.0.0.15"
            },
            "pg-cluster-02.example.com": {
                "ansible_host": "10.0.0.16"
            },
            "pg-cluster-03.example.com": {
                "ansible_host": "10.0.0.17"
            },
            "pg-standalone-01.example.com": {
                "ansible_host": "10.0.0.10"
            }
        }
    },
    "all": {
        "children": [
            "ungrouped",
            "pg_standalone_a",
            "pg_cluster_b"
        ]
    },
    "pg_cluster_b": {
        "children": [
            "pg_cluster_b_db",
            "pg_cluster_b_lb"
        ]
    },
    "pg_cluster_b_db": {
        "hosts": [
            "pg-cluster-01.example.com",
            "pg-cluster-02.example.com",
            "pg-cluster-03.example.com"
        ]
    },
    "pg_standalone_a": {
        "hosts": [
            "pg-standalone-01.example.com"
        ]
    }
}
```

</details>

### List the inventory as graph

`ansible-inventory -i testing_inventory.yml --graph`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
@all:
  |--@ungrouped:
  |--@pg_standalone_a:
  |  |--pg-standalone-01.example.com
  |--@pg_cluster_b:
  |  |--@pg_cluster_b_db:
  |  |  |--pg-cluster-01.example.com
  |  |  |--pg-cluster-02.example.com
  |  |  |--pg-cluster-03.example.com
  |  |--@pg_cluster_b_lb:
```

</details>

## ansible ad hoc commands

Ansible ad hoc commands allow for quick execution of tasks without writing a full playbook. These commands are useful for simple operations such as restarting services, copying files, or gathering system information across a large number of machines. Ad hoc commands are executed using the ansible command-line tool and can target individual hosts or groups defined in the inventory.

### Collect list of target hosts without executing any actions

`ansible all -i testing_inventory.yml -m ping --list-hosts`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
  hosts (4):
    pg-standalone-01.example.com
    pg-cluster-01.example.com
    pg-cluster-02.example.com
    pg-cluster-03.example.com
```

</details>

### Execute module against specific host

`ansible all -i pg-standalone-01.example.com, -m ping`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
pg-standalone-01.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.10"
    },
    "changed": false,
    "ping": "pong"
}
```

</details>

### Set verbosity level for debugging

`ansible all -i pg-standalone-01.example.com, -m ping -vvvvv`

`ansible all -i pg-standalone-01.example.com, -m ping -vvv`

`ansible all -i pg-standalone-01.example.com, -m ping -v`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
Using /etc/ansible/ansible.cfg as config file
pg-standalone-01.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.10"
    },
    "changed": false,
    "ping": "pong"
}
```

</details>

### Collect ansible facts about specific host

`ansible all -i pg-standalone-01.example.com, -m setup`

`ansible all -i pg-standalone-01.example.com, -m setup | egrep "^\s*\"ansible" | egrep -v "ssh_host_key"`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
        "ansible_all_ipv6_addresses": [
        "ansible_apparmor": {
        "ansible_architecture": "x86_64",
        "ansible_bios_date": "12/01/2006",
        "ansible_bios_vendor": "innotek GmbH",
        "ansible_bios_version": "VirtualBox",
        "ansible_board_asset_tag": "NA",
        "ansible_board_name": "VirtualBox",
        "ansible_board_serial": "NA",
        "ansible_board_vendor": "Oracle Corporation",
        "ansible_board_version": "1.2",
        "ansible_chassis_asset_tag": "NA",
        "ansible_chassis_serial": "NA",
        "ansible_chassis_vendor": "Oracle Corporation",
        "ansible_chassis_version": "NA",
        "ansible_cmdline": {
        "ansible_date_time": {
        "ansible_default_ipv4": {
        "ansible_default_ipv6": {
        "ansible_device_links": {
        "ansible_devices": {
        "ansible_distribution": "Ubuntu",
        "ansible_distribution_file_parsed": true,
        "ansible_distribution_file_path": "/etc/os-release",
        "ansible_distribution_file_variety": "Debian",
        "ansible_distribution_major_version": "22",
        "ansible_distribution_release": "jammy",
        "ansible_distribution_version": "22.04",
        "ansible_dns": {
        "ansible_domain": "",
        "ansible_effective_group_id": 1020,
        "ansible_effective_user_id": 1018,
        "ansible_enp0s3": {
        "ansible_enp0s8": {
        "ansible_env": {
        "ansible_fibre_channel_wwn": [],
        "ansible_fips": false,
        "ansible_form_factor": "Other",
        "ansible_fqdn": "pg-standalone-01",
        "ansible_hostname": "pg-standalone-01",
        "ansible_hostnqn": "",
        "ansible_interfaces": [
        "ansible_is_chroot": false,
        "ansible_iscsi_iqn": "",
        "ansible_kernel": "6.5.0-41-generic",
        "ansible_kernel_version": "#41~22.04.2-Ubuntu SMP PREEMPT_DYNAMIC Mon Jun  3 11:32:55 UTC 2",
        "ansible_lo": {
        "ansible_loadavg": {
        "ansible_local": {},
        "ansible_locally_reachable_ips": {
        "ansible_lsb": {
        "ansible_lvm": "N/A",
        "ansible_machine": "x86_64",
        "ansible_machine_id": "e753513a155341cc9b80d1912634f0a6",
        "ansible_memfree_mb": 357,
        "ansible_memory_mb": {
        "ansible_memtotal_mb": 3907,
        "ansible_mounts": [
        "ansible_nodename": "pg-standalone-01",
        "ansible_os_family": "Debian",
        "ansible_pkg_mgr": "apt",
        "ansible_proc_cmdline": {
        "ansible_processor": [
        "ansible_processor_cores": 1,
        "ansible_processor_count": 1,
        "ansible_processor_nproc": 1,
        "ansible_processor_threads_per_core": 1,
        "ansible_processor_vcpus": 1,
        "ansible_product_name": "VirtualBox",
        "ansible_product_serial": "NA",
        "ansible_product_uuid": "NA",
        "ansible_product_version": "1.2",
        "ansible_python": {
        "ansible_python_version": "3.10.12",
        "ansible_real_group_id": 1020,
        "ansible_real_user_id": 1018,
        "ansible_selinux": {
        "ansible_selinux_python_present": true,
        "ansible_service_mgr": "systemd",
        "ansible_swapfree_mb": 2047,
        "ansible_swaptotal_mb": 2047,
        "ansible_system": "Linux",
        "ansible_system_capabilities": [
        "ansible_system_capabilities_enforced": "True",
        "ansible_system_vendor": "innotek GmbH",
        "ansible_uptime_seconds": 100513,
        "ansible_user_dir": "/home/ansible",
        "ansible_user_gecos": "to be used by ansible",
        "ansible_user_gid": 1020,
        "ansible_user_id": "ansible",
        "ansible_user_shell": "/bin/bash",
        "ansible_user_uid": 1018,
        "ansible_userspace_architecture": "x86_64",
        "ansible_userspace_bits": "64",
        "ansible_virtualization_role": "guest",
        "ansible_virtualization_tech_guest": [
        "ansible_virtualization_tech_host": [],
        "ansible_virtualization_type": "virtualbox",
```

</details>

### Execute shell command with source the environment

`ansible all -i testing_inventory.yml -m shell -a "uptime"`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
pg-cluster-03.example.com | CHANGED | rc=0 >>
 01:19:45 up 6 days,  4:44,  1 user,  load average: 0.13, 0.07, 0.02
pg-cluster-02.example.com | CHANGED | rc=0 >>
 01:18:58 up 6 days,  4:44,  1 user,  load average: 0.10, 0.06, 0.01
pg-cluster-01.example.com | CHANGED | rc=0 >>
 23:22:18 up 7 days,  2:47,  3 users,  load average: 0.16, 0.12, 0.09
pg-standalone-01.example.com | CHANGED | rc=0 >>
 08:10:24 up 1 day,  3:56,  5 users,  load average: 0.00, 0.01, 0.00
```

</details>

### Execute command without source the environment

`ansible all -i testing_inventory.yml -m command -a "uptime"`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
pg-standalone-01.example.com | CHANGED | rc=0 >>
 08:11:54 up 1 day,  3:57,  5 users,  load average: 0.06, 0.02, 0.00
pg-cluster-02.example.com | CHANGED | rc=0 >>
 01:20:36 up 6 days,  4:46,  1 user,  load average: 0.18, 0.08, 0.01
pg-cluster-03.example.com | CHANGED | rc=0 >>
 01:21:23 up 6 days,  4:46,  1 user,  load average: 0.14, 0.10, 0.03
pg-cluster-01.example.com | CHANGED | rc=0 >>
 23:23:56 up 7 days,  2:49,  3 users,  load average: 0.48, 0.21, 0.12
```

</details>

### Use pipe with shell commands

`ansible all -i testing_inventory.yml -m shell -a "lscpu | egrep 'Architecture:'"`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
pg-cluster-02.example.com | CHANGED | rc=0 >>
Architecture:                       x86_64
pg-cluster-03.example.com | CHANGED | rc=0 >>
Architecture:                       x86_64
pg-cluster-01.example.com | CHANGED | rc=0 >>
Architecture:                       x86_64
pg-standalone-01.example.com | CHANGED | rc=0 >>
Architecture:                       x86_64
```

</details>

### Pipe failed with the `command` module

`ansible all -i pg-standalone-01.example.com, -m command -a "lscpu | egrep 'Architecture:'"`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
pg-standalone-01.example.com | FAILED | rc=1 >>
lscpu: bad usage
Try 'lscpu --help' for more information.non-zero return code
```

</details>

### Transfer file from local host to remote host

`ansible all -i pg-standalone-01.example.com, -m copy -a "src=source_file dest=/tmp"`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
pg-standalone-01.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.10"
    },
    "changed": false,
    "checksum": "da39a3ee5e6b4b0d3255bfef95601890afd80709",
    "dest": "/tmp/source_file",
    "gid": 1020,
    "group": "ansible",
    "mode": "0664",
    "owner": "ansible",
    "path": "/tmp/source_file",
    "size": 0,
    "state": "file",
    "uid": 1018
}
```

</details>


### Transfer file from remote host to local host

`ansible pg-standalone-01.example.com -m fetch -a "src=/var/lib/postgresql/16/testdb.tgz dest=/tmp/ flat=yes"`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
pg-standalone-01.example.com | CHANGED => {
    "changed": true,
    "checksum": "6949b21c5ccdff93c55fb7828b22fb74db25905a",
    "dest": "/tmp/testdb.tgz",
    "md5sum": "e6846f497b05cb9d193a2fd67aec3091",
    "remote_checksum": "6949b21c5ccdff93c55fb7828b22fb74db25905a",
    "remote_md5sum": null
}
```

</details>


### Delete file if it exists

`ansible all -i pg-standalone-01.example.com, -m file -a "path=/tmp/source_file state=absent"`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
pg-standalone-01.example.com | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.10"
    },
    "changed": true,
    "path": "/tmp/source_file",
    "state": "absent"
}
```

</details>

### Download file from URL to local directory

`ansible all -i pg-standalone-01.example.com, -m get_url -a "url=https://filesamples.com/samples/document/csv/sample4.csv dest=/tmp"`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
pg-standalone-01.example.com | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.10"
    },
    "changed": true,
    "checksum_dest": null,
    "checksum_src": "9199099354abc55cdf7f5aa7a153a17a619e10f0",
    "dest": "/tmp/sample4.csv",
    "elapsed": 0,
    "gid": 1020,
    "group": "ansible",
    "md5sum": "39a7a4186536ae2c6365d4f787e682bd",
    "mode": "0664",
    "msg": "OK (unknown bytes)",
    "owner": "ansible",
    "size": 7918,
    "src": "/home/ansible/.ansible/tmp/ansible-tmp-1720330249.029342-68634-207136633506269/tmprm6er30c",
    "state": "file",
    "status_code": 200,
    "uid": 1018,
    "url": "https://filesamples.com/samples/document/csv/sample4.csv"
}
```

</details>

### Check the accessibility of website

`ansible all -i pg-standalone-01.example.com, -m uri -a "url=https://ya.ru return_content=yes"`

`ansible all -i pg-standalone-01.example.com, -m uri -a "url=https://ya.ru"`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
pg-standalone-01.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.10"
    },
    "cache_control": "no-store, no-cache, must-revalidate, proxy-revalidate",
    "changed": false,
    "connection": "Close",
    "content_length": "1942",
    "content_security_policy": "default-src 'none'; frame-ancestors https://*.yandex.ru https://yandex.ru https://*.ya.ru https://ya.ru; connect-src 'self'; script-src 'nonce-e48db9b87a860bdc8eab4965d9df8941' 'self'; img-src 'self'",
    "content_type": "text/html; charset=utf-8",
    "cookies": {
        "_yasc": "80uei51/DmEg37DIvePDdxhxSWY2WzRsLz0uq2JbG4JPl2n+rNjxiNCcX4HQ8z/DXWE=",
        "i": "Wcp1sLFughx4Lz4PJCI6JBfJaak0wIxkVV1/3NTEbzKaiSMzesnh4qJeATEMq5u/HCIehHzPIumE8kAQsYARmbdBPFU=",
        "is_gdpr": "0",
        "is_gdpr_b": "CNa0CBCAhgIoAg==",
        "mda2_beacon": "1720330367740",
        "mda2_domains": "ya.ru",
        "receive-cookie-deprecation": "1",
        "yandex_csyr": "1720330367",
        "yandexuid": "8701856921720330367",
        "yashr": "6093916601720330367",
        "ys": "c_chck.656061142"
    },
    "cookies_string": "mda2_beacon=1720330367740; mda2_domains=ya.ru; _yasc=80uei51/DmEg37DIvePDdxhxSWY2WzRsLz0uq2JbG4JPl2n+rNjxiNCcX4HQ8z/DXWE=; i=H3rXNSJgu/lfCNgV5/wqRjQ/XQpFeg8sw/TlDfz/DZBNXfeyYW3dPhf/+N6BrVu7BDkCbQIL9Qc/lB8qNsn4xccuW+4=; is_gdpr=0; is_gdpr_b=CNa0CBCAhgIoAg==; receive-cookie-deprecation=1; yandex_csyr=1720330367; yandexuid=8972331541720330367; yashr=6093916601720330367; i=Wcp1sLFughx4Lz4PJCI6JBfJaak0wIxkVV1/3NTEbzKaiSMzesnh4qJeATEMq5u/HCIehHzPIumE8kAQsYARmbdBPFU=; yandexuid=8701856921720330367; ys=c_chck.656061142",
    "date": "Sun, 07 Jul 2024 05:32:47 GMT",
    "elapsed": 0,
    "etag": "W/\"796-M3UhAWDIgmAcvcGJyAsBI7Botcs\"",
    "expires": "0",
    "msg": "OK (1942 bytes)",
    "pragma": "no-cache",
    "redirected": true,
    "referrer_policy": "origin",
    "set_cookie": "mda2_beacon=1720330367740; Domain=.passport.yandex.ru; Expires=Tue, 19 Jan 2038 03:14:07 GMT; Secure; Path=/, ys=c_chck.656061142; Domain=.yandex.ru; Secure; Path=/, i=Wcp1sLFughx4Lz4PJCI6JBfJaak0wIxkVV1/3NTEbzKaiSMzesnh4qJeATEMq5u/HCIehHzPIumE8kAQsYARmbdBPFU=; Domain=.yandex.ru; Expires=Wed, 05 Jul 2034 05:32:47 GMT; Secure; HttpOnly; Path=/, yandexuid=8701856921720330367; Domain=.yandex.ru; Expires=Wed, 05 Jul 2034 05:32:47 GMT; Secure; Path=/, mda2_domains=ya.ru; Domain=.passport.yandex.ru; Expires=Tue, 19 Jan 2038 03:14:07 GMT; Secure; Path=/",
    "status": 200,
    "strict_transport_security": "max-age=315360000; includeSubDomains; preload",
    "surrogate_control": "no-store",
    "url": "https://sso.passport.yandex.ru/push?retpath=https%3A%2F%2Fya.ru%2F%3Fnr%3D1%26redirect_ts%3D1720330367.00000&uuid=185b1700-2c77-4a25-aefa-901d33b60026",
    "x_content_type_options": "nosniff",
    "x_dns_prefetch_control": "off",
    "x_download_options": "noopen",
    "x_e": "d",
    "x_xss_protection": "1; mode=block"
}
```

</details>

### Execute module with administrative privileges

`ansible all -i pg-standalone-01.example.com, -m service -a "name=apache2 state=stopped enabled=no" -b`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
pg-standalone-01.example.com | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.10"
    },
    "changed": true,
    "enabled": false,
    "name": "apache2",
    "state": "stopped",
    "status": {
        "ActiveEnterTimestamp": "n/a",
        "ActiveEnterTimestampMonotonic": "0",
        "ActiveExitTimestamp": "n/a",
        "ActiveExitTimestampMonotonic": "0",
        "ActiveState": "failed",

(... Output truncated intentionally ...)
```

</details>

## ansible-vault

`ansible-vault` is a feature of Ansible that enables secure encryption and decryption of sensitive data. With `ansible-vault`, users can encrypt passwords, keys, and other confidential information within playbooks and roles. This ensures that sensitive data remains protected at rest and can only be accessed by authorized individuals who possess the decryption key.

### Create new encrypted file

`ansible-vault create secret_file.txt`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
New Vault password:
Confirm New Vault password:
```

</details>

### View encrypted file

`ansible-vault view secret_file.txt`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
Vault password:
my-secret
```

</details>

### Edit encrypted file

`ansible-vault edit secret_file.txt`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
Vault password:
```

</details>

### Change encryption key of encrypted file

`ansible-vault rekey secret_file.txt`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
Vault password:
New Vault password:
Confirm New Vault password:
Rekey successful
```

</details>

### Encrypt playbook file

`ansible-vault encrypt secret_playbook.yml`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
New Vault password:
Confirm New Vault password:
Encryption successful
```

</details>

### Execute encrypted playbook file

`ansible-playbook secret_playbook.yml --ask-vault-password`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
Vault password:

PLAY [Test connection to servers] ***********************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Print Hello] **************************************************************************************************************************************************
ok: [pg-standalone-01.example.com] => {
    "msg": "Hello, my dear friend!"
}

TASK [Ping my servers] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

`ansible-playbook secret_playbook.yml --vault-password-file password_file.txt`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [Test connection to servers] ***********************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Print Hello] **************************************************************************************************************************************************
ok: [pg-standalone-01.example.com] => {
    "msg": "Hello, my dear friend!"
}

TASK [Ping my servers] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Decrypt playbook file

`ansible-vault decrypt secret_playbook.yml`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
Vault password:
Decryption successful
```

</details>

### Encrypt string

`ansible-vault encrypt_string --stdin-name "My password"`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
New Vault password:
Confirm New Vault password:
Reading plaintext input from stdin. (ctrl-d to end input, twice if your content does not already have a newline)

Encryption successful
My password: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          38623931383431643537616538333661396536316531313066346263323933353437653165643734
          3935333064393166653061393339306664656536303138330a373361373937663233306332643831
          38623030303564306262306164343637343538336462346330306165373832383762386236303937
          3333363136346662350a316331323664376364386261353438386662396166323930653333623062
          6539
```

</details>

## ansible-playbook

`ansible-playbook` is the core command-line tool for running Ansible playbooks. Playbooks are [YAML scripts](https://www.freecodecamp.org/news/what-is-yaml-the-yml-file-format/) that describe automation tasks for managing configurations and deploying software across a fleet of machines. `ansible-playbook` orchestrates the execution of these tasks, applying them in order to achieve the desired state of the infrastructure.

### Check syntax of playbook

`ansible-playbook testing_playbook.yml --syntax-check`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
playbook: testing_playbook.yml
```

</details>

`ansible-playbook wrong_playbook.yml --syntax-check`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
ERROR! couldn't resolve module/action 'wrong_module'. This often indicates a misspelling, missing collection, or incorrect module path.

The error appears to be in '/private/etc/ansible/playbooks/wrong_playbook.yml': line 12, column 5, but may
be elsewhere in the file depending on the exact syntax problem.

The offending line appears to be:


  - name: Wrong module
    ^ here
```

</details>

### List hosts, tags, and tasks defined in playbook

`ansible-playbook -i testing_inventory.yml testing_playbook.yml --list-hosts --list-tags --list-tasks`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
playbook: testing_playbook.yml

  play #1 (all): Test connection to servers     TAGS: []
    pattern: ['all']
    hosts (4):
      pg-cluster-01.example.com
      pg-cluster-02.example.com
      pg-standalone-01.example.com
      pg-cluster-03.example.com
    tasks:
      Print Hello       TAGS: []
      Ping my servers   TAGS: [check]
      TASK TAGS: [check]
```

</details>

### Perform dry run of playbook, no actual changes

`ansible-playbook -i testing_inventory.yml testing_playbook.yml --check`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [Test connection to servers] ***********************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-cluster-03.example.com]
ok: [pg-cluster-01.example.com]
ok: [pg-cluster-02.example.com]
ok: [pg-standalone-01.example.com]

TASK [Print Hello] **************************************************************************************************************************************************
ok: [pg-standalone-01.example.com] => {
    "msg": "Hello, my dear friend!"
}
ok: [pg-cluster-01.example.com] => {
    "msg": "Hello, my dear friend!"
}
ok: [pg-cluster-02.example.com] => {
    "msg": "Hello, my dear friend!"
}
ok: [pg-cluster-03.example.com] => {
    "msg": "Hello, my dear friend!"
}

TASK [Ping my servers] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-03.example.com]
ok: [pg-cluster-01.example.com]
ok: [pg-cluster-02.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-cluster-01.example.com    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-02.example.com    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-03.example.com    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-standalone-01.example.com          : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Execute playbook on specific group of hosts

`ansible-playbook -i testing_inventory.yml testing_playbook.yml -l standalone`

<details>
  <summary>Example Output (Click to expand)</summary>

```json

PLAY [Test connection to servers] ***********************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Print Hello] **************************************************************************************************************************************************
ok: [pg-standalone-01.example.com] => {
    "msg": "Hello, my dear friend!"
}

TASK [Ping my servers] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Run playbook but only execute tasks tagged with 'my_tag'

`ansible-playbook -i testing_inventory.yml testing_playbook.yml -t check`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [Test connection to servers] ***********************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-02.example.com]
ok: [pg-cluster-01.example.com]
ok: [pg-cluster-03.example.com]

TASK [Ping my servers] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-02.example.com]
ok: [pg-cluster-01.example.com]
ok: [pg-cluster-03.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-cluster-01.example.com    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-02.example.com    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-03.example.com    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-standalone-01.example.com          : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Start executing playbook at specific task

`ansible-playbook -i testing_inventory.yml testing_playbook.yml --start-at-task "Ping my servers"`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [Test connection to servers] ***********************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-cluster-01.example.com]
ok: [pg-cluster-03.example.com]
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-02.example.com]

TASK [Ping my servers] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-01.example.com]
ok: [pg-cluster-03.example.com]
ok: [pg-cluster-02.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-cluster-01.example.com    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-02.example.com    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-03.example.com    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-standalone-01.example.com          : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Execute playbook steps by step

`ansible-playbook -i testing_inventory.yml testing_playbook.yml --step`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [Test connection to servers] ***********************************************************************************************************************************
Perform task: TASK: Gathering Facts (N)o/(y)es/(c)ontinue: y

Perform task: TASK: Gathering Facts (N)o/(y)es/(c)ontinue: **********************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-01.example.com]
ok: [pg-cluster-02.example.com]
ok: [pg-cluster-03.example.com]
Perform task: TASK: Print Hello (N)o/(y)es/(c)ontinue: n

Perform task: TASK: Print Hello (N)o/(y)es/(c)ontinue: **************************************************************************************************************
Perform task: TASK: Ping my servers (N)o/(y)es/(c)ontinue: c

Perform task: TASK: Ping my servers (N)o/(y)es/(c)ontinue: **********************************************************************************************************

TASK [Ping my servers] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-02.example.com]
ok: [pg-cluster-01.example.com]
ok: [pg-cluster-03.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-cluster-01.example.com    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-02.example.com    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-03.example.com    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-standalone-01.example.com          : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Execute playbook

`ansible-playbook testing_playbook.yml -i testing_inventory.yml -u "my_remote_user" -Kk`

<details>
  <summary>Example Output (Click to expand)</summary>

```json
SSH password:
BECOME password[defaults to SSH password]:

PLAY [Test connection to servers] ***********************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-cluster-02.example.com]
ok: [pg-cluster-03.example.com]
ok: [pg-cluster-01.example.com]
ok: [pg-standalone-01.example.com]

TASK [Print Hello] **************************************************************************************************************************************************
ok: [pg-standalone-01.example.com] => {
    "msg": "Hello, my dear friend!"
}
ok: [pg-cluster-01.example.com] => {
    "msg": "Hello, my dear friend!"
}
ok: [pg-cluster-02.example.com] => {
    "msg": "Hello, my dear friend!"
}
ok: [pg-cluster-03.example.com] => {
    "msg": "Hello, my dear friend!"
}

TASK [Ping my servers] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-02.example.com]
ok: [pg-cluster-03.example.com]
ok: [pg-cluster-01.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-cluster-01.example.com    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-02.example.com    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-03.example.com    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-standalone-01.example.com          : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

## ansible usefull modules

Ansible modules are units of code that perform specific tasks. There is a lot of modules available, covering a wide range of functionality from file management and network configuration to cloud service interactions. Modules are designed to be [idempotent](https://docs.ansible.com/ansible/latest/reference_appendices/glossary.html#term-Idempotency), meaning they can be applied multiple times without changing the result beyond the initial application. This section of the cheat sheet highlights some of the most usefull modules, providing a quick reference for everyday tasks.

The basic setup to test modules is listed below:

```bash
# Contents of Ansible inventory
$ cat testing_inventory
---
all:
  children:

    ############################
    # grouped by installations #
    ############################

    ## postgres
    ############################
    pg_standalone_a:
      hosts:
        pg-standalone-01.example.com:
          ansible_host: 10.0.0.10
    pg_cluster_b:
      children:
        pg_cluster_b_db:
          hosts:
            pg-cluster-01.example.com:
              ansible_host: 10.0.0.15
            pg-cluster-02.example.com:
              ansible_host: 10.0.0.16
            pg-cluster-03.example.com:
              ansible_host: 10.0.0.17
        pg_cluster_b_lb:
          hosts:
      hosts:

# Run Ansible playbook for all hosts
$ ansible-playbook -i testing_inventory testing_modules.yml

# Run Ansible playbook for specific host
$ ansible-playbook -i testing_inventory testing_modules.yml -l pg-standalone-01.example.com
```

### Module ping

```yaml
---
- name: Ping module
  hosts: all
  become: True
  tasks:
    - name: Test connection
      ping:
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [Ping module] **************************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-cluster-02.example.com]
ok: [pg-cluster-03.example.com]
ok: [pg-cluster-01.example.com]
ok: [pg-standalone-01.example.com]

TASK [Test connection] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-01.example.com]
ok: [pg-cluster-02.example.com]
ok: [pg-cluster-03.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-cluster-01.example.com    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-02.example.com    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-03.example.com    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-standalone-01.example.com          : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module setup

```bash
ansible all -i testing_inventory.yml -m setup -a 'filter=ansible_os_family'
```
<details>
  <summary>Example Output (Click to expand)</summary>

```json
pg-cluster-03.example.com | SUCCESS => {
    "ansible_facts": {
        "ansible_os_family": "RedHat",
        "discovered_interpreter_python": "/usr/bin/python3.9"
    },
    "changed": false
}
pg-cluster-02.example.com | SUCCESS => {
    "ansible_facts": {
        "ansible_os_family": "RedHat",
        "discovered_interpreter_python": "/usr/bin/python3.9"
    },
    "changed": false
}
pg-cluster-01.example.com | SUCCESS => {
    "ansible_facts": {
        "ansible_os_family": "RedHat",
        "discovered_interpreter_python": "/usr/bin/python3.9"
    },
    "changed": false
}
pg-standalone-01.example.com | SUCCESS => {
    "ansible_facts": {
        "ansible_os_family": "Debian",
        "discovered_interpreter_python": "/usr/bin/python3.10"
    },
    "changed": false
}
```

</details>

### Module apt

`ansible all -i pg-standalone-01.example.com, -m yum -a "name=iputils-ping state=present" -b`

```yaml
---
- name: Testing apt module
  hosts: all
  become: True
  tasks:
    - name: Remove iotop on Debian-based OS
      apt:
        name: iotop
        state: absent
      when: ansible_os_family == "Debian"
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [Testing apt module] *******************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-cluster-02.example.com]
ok: [pg-cluster-03.example.com]
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-01.example.com]

TASK [Remove iotop on Debian-based OS] ******************************************************************************************************************************
skipping: [pg-cluster-01.example.com]
skipping: [pg-cluster-02.example.com]
skipping: [pg-cluster-03.example.com]
changed: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-cluster-01.example.com    : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
pg-cluster-02.example.com    : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
pg-cluster-03.example.com    : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
pg-standalone-01.example.com          : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module yum

```yaml
---
- name: Testing yum module
  hosts: all
  become: True
  tasks:
    - name: Remove iotop on Redhat-based OS
      yum:
        name: iotop
        state: absent
      when: ansible_os_family == "RedHat"
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [Testing yum module] *******************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-cluster-01.example.com]
ok: [pg-cluster-02.example.com]
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-03.example.com]

TASK [Remove iotop on Redhat-based OS] ******************************************************************************************************************************
skipping: [pg-standalone-01.example.com]
changed: [pg-cluster-02.example.com]
changed: [pg-cluster-01.example.com]
changed: [pg-cluster-03.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-cluster-01.example.com    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-02.example.com    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-cluster-03.example.com    : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
pg-standalone-01.example.com          : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
```

</details>

### Module package

```yaml
---
- name: Testing package module
  hosts: all
  become: True
  tasks:

  - name: Install iotop on Debian-based OS
    package:
      name: iotop
      state: present
    when: ansible_os_family == "Debian"

  - name: Install iotop on Redhat-based OS
    package:
      name: iotop
      state: present
      sslverify: false
    when: ansible_os_family == "RedHat"
```
<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [Testing package module] ***************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-cluster-03.example.com]
ok: [pg-cluster-01.example.com]
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-02.example.com]

TASK [Install iotop on Debian-based OS] *****************************************************************************************************************************
skipping: [pg-cluster-01.example.com]
skipping: [pg-cluster-02.example.com]
skipping: [pg-cluster-03.example.com]
changed: [pg-standalone-01.example.com]

TASK [Install iotop on Redhat-based OS] *****************************************************************************************************************************
skipping: [pg-standalone-01.example.com]
changed: [pg-cluster-03.example.com]
changed: [pg-cluster-02.example.com]
changed: [pg-cluster-01.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-cluster-01.example.com    : ok=2    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
pg-cluster-02.example.com    : ok=2    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
pg-cluster-03.example.com    : ok=2    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
pg-standalone-01.example.com          : ok=2    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
```

</details>

### Module pip

```yaml
---
- name: Update python packages
  hosts: all
  become: True
  tasks:
  - name: Install multi python packages with version specifiers
    pip:
      name:
        - django>1.11.0,<1.12.0
        - bottle>0.10,<0.20,!=0.11
    when: ansible_os_family == "Debian"
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [Update python packages] ***************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-cluster-03.example.com]
ok: [pg-cluster-02.example.com]
ok: [pg-standalone-01.example.com]
ok: [pg-cluster-01.example.com]

TASK [Install multi python packages with version specifiers] ********************************************************************************************************
skipping: [pg-cluster-01.example.com]
skipping: [pg-cluster-02.example.com]
skipping: [pg-cluster-03.example.com]
changed: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-cluster-01.example.com    : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
pg-cluster-02.example.com    : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
pg-cluster-03.example.com    : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
pg-standalone-01.example.com          : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module raw

```yaml
---
- name: raw module usage
  hosts: all
  become: True
  tasks:
  - name: Bootstrap a host without python installed
    raw: apt install -y python2

  - name: Run a command that uses non-posix shell-isms (in this example /bin/sh doesn't handle redirection and wildcards together but bash does)
    raw: cat < /tmp/*txt
    args:
      executable: /bin/bash
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [raw module usage] *********************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Bootstrap a host without python installed] ********************************************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [Run a command that uses non-posix shell-isms (in this example /bin/sh doesn't handle redirection and wildcards together but bash does)] ***********************
changed: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module command

```yaml
---
- name: command module
  hosts: all
  become: True
  tasks:

  - name: Check Postgres version
    command: su -c "/usr/lib/postgresql/16/bin/psql -p 5432 -At -c \"select version()\"" -l postgres
    register: pg_version
    changed_when: no

  - name: Show Postgres version
    debug:
      var: pg_version.stdout_lines
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [command module] ***********************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Check Postgres version] ***************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Show Postgres version] ****************************************************************************************************************************************
ok: [pg-standalone-01.example.com] => {
    "pg_version.stdout_lines": [
        "!!! postgres: start the shell with an environment !!!",
        "PostgreSQL 15.6 (Ubuntu 15.6-1.pgdg22.04+1) on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 11.4.0-1ubuntu1~22.04) 11.4.0, 64-bit",
        "Time: 0,083 ms"
    ]
}

PLAY RECAP **********************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module shell

```yaml
---
- name: shell module
  hosts: all
  become: True
  tasks:

  - name: Check Postgres version
    shell: su -c "/usr/lib/postgresql/16/bin/psql -p 5432 -At -c \"select version()\"" -l postgres > /tmp/pg_check_version.txt

  - name: Get Postgres version
    shell: cat /tmp/pg_check_version.txt
    register: pg_version

  - name: Show Postgres version
    debug:
      var: pg_version.stdout_lines
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [shell module] *************************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Check Postgres version] ***************************************************************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [Get Postgres version] *****************************************************************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [Show Postgres version] ****************************************************************************************************************************************
ok: [pg-standalone-01.example.com] => {
    "pg_version.stdout_lines": [
        "!!! postgres: start the shell with an environment !!!",
        "PostgreSQL 15.6 (Ubuntu 15.6-1.pgdg22.04+1) on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 11.4.0-1ubuntu1~22.04) 11.4.0, 64-bit",
        "Time: 0,083 ms"
    ]
}

PLAY RECAP **********************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module script


```yaml
---
- name: script module
  hosts: all
  tasks:
  -  name: Run a script with arguments
     script: testing_script.sh some_parameter
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [script module] ************************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Run a script with arguments] **********************************************************************************************************************************
changed: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module copy

```yaml
---
- name: copy module
  hosts: all
  tasks:

  - name: copy a file from local host to local host
    copy:
      src: files/src.txt
      dest: files/dest.txt
    delegate_to: localhost

  - name: copy a file from remote host to remote host
    copy:
      src: /tmp/src.txt
      dest: /tmp/dest.txt
      remote_src: yes

  - name: copy a file from local host to remote host with owner and permissions
    copy:
      src: files/src.txt
      dest: /tmp/dest2.txt
      owner: postgres
      group: backup
      mode: '0644'
    become: yes
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [copy module] **************************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [copy a file from local host to local host] ********************************************************************************************************************
changed: [pg-standalone-01.example.com -> localhost]

TASK [copy a file from remote host to remote host] ******************************************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [copy a file from local host to remote host with owner and permissions] ****************************************************************************************
changed: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=4    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module fetch

```yaml
---
- name: fetch module
  hosts: all
  become: True
  tasks:

  - name: copy a file from remote host to local host
    fetch:
      src: /var/log/postgresql/postgresql-15-testdb.log
      dest: /tmp/fetched

  - name: copy a file from remote host to local host without parent folder structure.
    fetch:
      src: /var/log/postgresql/postgresql-15-testdb.log
      #dest: /tmp/{{ inventory_hostname }}/
      dest: /tmp/{{ ansible_hostname }}/
      flat: true
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [fetch module] *************************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [copy a file from remote host to local host] *******************************************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [copy a file from remote host to local host without parent folder structure.] **********************************************************************************
changed: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

```bash
$ tree /tmp/fetched
/tmp/fetched
└── pg-standalone-01.example.com
    └── var
        └── log
            └── postgresql
                └── postgresql-15-testdb.log

4 directories, 1 file

$ tree /tmp/pg-standalone-01
/tmp/pg-standalone-01
└── postgresql-15-testdb.log

0 directories, 1 file
```

</details>

### Module get_url

```yaml
---
- name: get_url module
  hosts: all
  become: True
  tasks:

  - name: download sample test file
    get_url:
      url: https://sampletestfile.com/wp-content/uploads/2023/07/500KB-CSV.csv
      dest: /tmp/sampletestfile.csv
      mode: 0755
      owner: postgres
      group: backup
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [get_url module] *******************************************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [download sample test file] ********************************************************************************************************************************
ok: [pg-standalone-01.example.com]

PLAY RECAP ******************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module archive

```yaml
---
- name: archive module
  hosts: all
  become: True
  tasks:

  - name: Compress directory /var/lib/postgresql/16/testdb/ into /var/lib/postgresql/16/testdb.tgz
    archive:
      path: /var/lib/postgresql/16/testdb
      dest: /var/lib/postgresql/16/testdb.tgz

  - name: Compress regular file /tmp/sampletestfile.csv into /tmp/sampletestfile.csv.gz and remove it
    archive:
      path: /tmp/sampletestfile.csv
      remove: yes

  - name: Create a bz2 archive of multiple files, rooted at /var
    archive:
      path:
      - /var/lib/postgresql/16/testdb/postgresql.auto.conf
      - /var/lib/postgresql/16/testdb/postgresql.conf
      dest: /tmp/dest_file.tar.bz2
      format: bz2

  - name: Create a gz archive of a globbed path, while excluding specific dirnames
    archive:
      path:
      - /var/log/postgresql/*
      dest: /tmp/postgresql_logs.tar.gz
      exclude_path:
      - /var/log/postgresql/dir_to_exclude1
      - /var/log/postgresql/dir_to_exclude2
      format: gz
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [archive module] *******************************************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Compress directory /var/lib/postgresql/16/testdb/ into /var/lib/postgresql/16/testdb.tgz] *****************************************************************
changed: [pg-standalone-01.example.com]

TASK [Compress regular file /tmp/sampletestfile.csv into /tmp/sampletestfile.csv.gz and remove it] **************************************************************
changed: [pg-standalone-01.example.com]

TASK [Create a bz2 archive of multiple files, rooted at /var] ***************************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [Create a gz archive of a globbed path, while excluding specific dirnames] *********************************************************************************
changed: [pg-standalone-01.example.com]

PLAY RECAP ******************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=5    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module unarchive

```yaml
---
- name: unarchive module
  hosts: all
  become: True
  tasks:

  - name: Extract tgz file into destination directory
    unarchive:
      src: /tmp/testdb.tgz
      dest: /tmp

  - name: Unarchive a file that is already on the remote host
    unarchive:
      src: /var/lib/postgresql/16/testdb.tgz
      dest: /var/lib/postgresql/16
      group: postgres
      owner: postgres
      mode: '0750'
      remote_src: yes

  - name: Unarchive a file that needs to be downloaded
    unarchive:
      src: https://dlcdn.apache.org/httpd/httpd-2.4.61.tar.gz
      dest: /tmp
      remote_src: yes
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [unarchive module] *****************************************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Extract tgz file into destination directory] **************************************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [Unarchive a file that is already on the remote host] ******************************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [Unarchive a file that needs to be downloaded] *************************************************************************************************************
changed: [pg-standalone-01.example.com]

PLAY RECAP ******************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=4    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module file

```yaml
---
- name: file module
  hosts: all
  become: True
  tasks:

  - name: Create a directory if it does not exist
    file:
      path: /tmp/some_directory
      state: directory
      mode: '0755'

  - name: Create a file
    file:
      path: /tmp/foo.conf
      state: touch
      mode: u=rw,g=r,o=r

  - name: Change file ownership, group and permissions
    file:
      path: /tmp/foo.conf
      group: postgres
      owner: postgres
      mode: '0644'

  - name: Create a symbolic link
    file:
      src: /tmp/foo.conf
      dest: /tmp/symlink
      owner: postgres
      group: postgres
      state: link

  - name: Remove file (delete file)
    file:
      path: /tmp/foo.conf
      state: absent
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json

PLAY [file module] **********************************************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Create a directory if it does not exist] ******************************************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [Create a file] ********************************************************************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [Change file ownership, group and permissions] *************************************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [Create a symbolic link] ***********************************************************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [Remove file (delete file)] ********************************************************************************************************************************
changed: [pg-standalone-01.example.com]

PLAY RECAP ******************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=6    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module template

```bash
cat <<'EOF'> templates/pgbouncer_small_example_config.ini
; Small example config for Pgbouncer
; taken from https://www.pgbouncer.org/config.html
[databases]
{{ pgbouncer_dbname }} = host={{ ansible_hostname }} dbname={{ pgbouncer_dbname }} auth_user={{ pgbouncer_auth_user }}

[pgbouncer]
pool_mode = {{ pgbouncer_pool_mode }}
listen_port = {{ pgbouncer_listen_port }}
listen_addr = {{ ansible_hostname }}
auth_type = md5
auth_file = users.txt
logfile = pgbouncer.log
pidfile = pgbouncer.pid
admin_users = {{ pgbouncer_auth_user }}
stats_users = stat_collector
EOF
```

```yaml
---
- name: template module
  hosts: all
  become: True
  vars:
    pgbouncer_pool_mode: transaction
    pgbouncer_listen_port: 6432
  tasks:

  - name: Template a file to /etc/pgbouncer/pgbouncer.ini
    template:
      src: pgbouncer_small_example_config.ini
      dest: /etc/pgbouncer/pgbouncer.ini
      group: postgres
      owner: postgres
      mode: '0600'
    vars:
      pgbouncer_pool_mode: session
      pgbouncer_listen_port: 6432
      pgbouncer_dbname: postgres
      pgbouncer_auth_user: pgbouncer
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [template module] ******************************************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Template a file to /etc/pgbouncer/pgbouncer.ini] **********************************************************************************************************
changed: [pg-standalone-01.example.com]

PLAY RECAP ******************************************************************************************************************************************************
pg-standalone-01.example.com          : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

```bash
$ cat pgbouncer.ini
; Small example config for Pgbouncer
; taken from https://www.pgbouncer.org/config.html
[databases]
postgres = host=pg-standalone-01 dbname=postgres auth_user=pgbouncer

[pgbouncer]
pool_mode = session
listen_port = 6432
listen_addr = pg-standalone-01
auth_type = md5
auth_file = users.txt
logfile = pgbouncer.log
pidfile = pgbouncer.pid
admin_users = pgbouncer
stats_users = stat_collector
```
</details>

### Module find

```yaml
---
- name: find module
  hosts: all
  become: true
  vars:
    ansible_find_files_age: 99d
  tasks:

  - name: Find old compressed Postgres logs older {{ ansible_find_files_age }}
    find:
      paths: /var/log/postgresql
      patterns: "postgresql-1[3-4]*[6-8].gz"
      age: "{{ ansible_find_files_age }}"
      # age_stamp: mtime
      # size: 1m
      recurse: no
      file_type: file
    register: output

  - name: Display found files
    debug:
      # var: item.path
      msg: "{{ item.path }}"
    loop: "{{ output.files }}"
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [find module] **************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Find old compressed Postgres logs older 99d] ******************************************************************
ok: [pg-standalone-01.example.com]

TASK [Display found files] ******************************************************************************************
ok: [pg-standalone-01.example.com] => (item={'path': '/var/log/postgresql/postgresql-14-main.log.6.gz', 'mode': '0640', 'isdir': False, 'ischr': False, 'isblk': False, 'isreg': True, 'isfifo': False, 'islnk': False, 'issock': False, 'uid': 1000, 'gid': 1000, 'size': 3432, 'inode': 926049, 'dev': 2051, 'nlink': 1, 'atime': 1720954538.285216, 'mtime': 1712410740.3600552, 'ctime': 1720904401.923801, 'gr_name': 'postgres', 'pw_name': 'postgres', 'wusr': True, 'rusr': True, 'xusr': False, 'wgrp': False, 'rgrp': True, 'xgrp': False, 'woth': False, 'roth': False, 'xoth': False, 'isuid': False, 'isgid': False}) => {
    "msg": "/var/log/postgresql/postgresql-14-main.log.6.gz"
}
ok: [pg-standalone-01.example.com] => (item={'path': '/var/log/postgresql/postgresql-14-main.log.8.gz', 'mode': '0640', 'isdir': False, 'ischr': False, 'isblk': False, 'isreg': True, 'isfifo': False, 'islnk': False, 'issock': False, 'uid': 1000, 'gid': 1000, 'size': 2040, 'inode': 920064, 'dev': 2051, 'nlink': 1, 'atime': 1720954538.285216, 'mtime': 1710671008.229001, 'ctime': 1720904401.923801, 'gr_name': 'postgres', 'pw_name': 'postgres', 'wusr': True, 'rusr': True, 'xusr': False, 'wgrp': False, 'rgrp': True, 'xgrp': False, 'woth': False, 'roth': False, 'xoth': False, 'isuid': False, 'isgid': False}) => {
    "msg": "/var/log/postgresql/postgresql-14-main.log.8.gz"
}
ok: [pg-standalone-01.example.com] => (item={'path': '/var/log/postgresql/postgresql-13-main.log.8.gz', 'mode': '0640', 'isdir': False, 'ischr': False, 'isblk': False, 'isreg': True, 'isfifo': False, 'islnk': False, 'issock': False, 'uid': 1013, 'gid': 1000, 'size': 454, 'inode': 920066, 'dev': 2051, 'nlink': 1, 'atime': 1720954538.2812161, 'mtime': 1712410740.312157, 'ctime': 1720904401.9118016, 'gr_name': 'postgres', 'pw_name': 'postgres13', 'wusr': True, 'rusr': True, 'xusr': False, 'wgrp': False, 'rgrp': True, 'xgrp': False, 'woth': False, 'roth': False, 'xoth': False, 'isuid': False, 'isgid': False}) => {
    "msg": "/var/log/postgresql/postgresql-13-main.log.8.gz"
}
ok: [pg-standalone-01.example.com] => (item={'path': '/var/log/postgresql/postgresql-14-main.log.7.gz', 'mode': '0640', 'isdir': False, 'ischr': False, 'isblk': False, 'isreg': True, 'isfifo': False, 'islnk': False, 'issock': False, 'uid': 1000, 'gid': 1000, 'size': 1899, 'inode': 919889, 'dev': 2051, 'nlink': 1, 'atime': 1720954538.285216, 'mtime': 1711290466.2309537, 'ctime': 1720904401.923801, 'gr_name': 'postgres', 'pw_name': 'postgres', 'wusr': True, 'rusr': True, 'xusr': False, 'wgrp': False, 'rgrp': True, 'xgrp': False, 'woth': False, 'roth': False, 'xoth': False, 'isuid': False, 'isgid': False}) => {
    "msg": "/var/log/postgresql/postgresql-14-main.log.7.gz"
}

PLAY RECAP **********************************************************************************************************
pg-standalone-01.example.com          : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module replace

```yaml
---
- name: replace module
  hosts: all
  become: True
  vars:
    pg_hba_file: /etc/postgresql/14/testdb/pg_hba.conf
  tasks:

  - name: Ansible replace md5 with scram-sha-256
    replace:
      path: "{{ pg_hba_file }}"
      regexp: 'md5'
      replace: 'scram-sha-256'

  - name: Replace between the expressions and create a backup
    replace:
      path: "{{ pg_hba_file }}"
      after: '# Custom settings: begin'
      before: '# Custom settings: end'
      regexp: 'all\s+all'
      replace: 'all\s+postgres'
      backup: yes
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [replace module] ***********************************************************************************************

TASK [Gathering Facts] **********************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Ansible replace md5 with scram-sha-256] ***********************************************************************
changed: [pg-standalone-01.example.com]

TASK [Replace between the expressions and create a backup] **********************************************************
changed: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************
pg-standalone-01.example.com          : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module lineinfile

```yaml
---
- name: lineinfile module
  hosts: all
  become: True
  vars:
    pg_config_file: /var/lib/postgresql/16/testdb/postgresql.conf
  tasks:

  - name: adding a line - set max_connections in postgresql.conf
    lineinfile:
      path: "{{ pg_config_file }}"
      regexp: '^max_connections ='
      line: max_connections = 200
      validate: 'egrep -q "^max_connections\s*=\s*[0-9]+" %s'

  - name: replacing a line
    lineinfile:
      path: "{{ pg_config_file }}"
      regexp: '^listen_addresses ='
      line: listen_addresses = '*'

  - name: replace a line only after a specified string
    lineinfile:
      path: "{{ pg_config_file }}"
      regexp: '^# Custom settings'
      insertafter: '^# Custom settings'
      line: max_connections = 300

  - name: deleting a line
    lineinfile:
      path: "{{ pg_config_file }}"
      regexp: '^full_page_writes ='
      state: absent
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [lineinfile module] ********************************************************************************************

TASK [Gathering Facts] **********************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [adding a line - set max_connections in postgresql.conf] *******************************************************
changed: [pg-standalone-01.example.com]

TASK [replacing a line] *********************************************************************************************
changed: [pg-standalone-01.example.com]

TASK [replace a line only after a specified string] *****************************************************************
changed: [pg-standalone-01.example.com]

TASK [deleting a line] **********************************************************************************************
changed: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************
pg-standalone-01.example.com          : ok=5    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module blockinfile

```yaml
---
- name: blockinfile module
  hosts: all
  become: True
  vars:
    pg_config_file: /var/lib/postgresql/16/testdb/postgresql.conf
  tasks:

  - name:
    blockinfile:
      path: "{{ pg_config_file }}"
      marker: '# ANSIBLE MANAGED BLOCK: {mark}'
      insertafter: '^# Custom settings'
      block: |
        max_connections = 400
        shared_buffers = '2048 MB'
        work_mem = '32 MB'
      backup: yes
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [blockinfile module] *******************************************************************************************

TASK [Gathering Facts] **********************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [blockinfile] **************************************************************************************************
changed: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************
pg-standalone-01.example.com          : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module cron

```yaml
---
- name: cron module
  hosts: all
  become: True

  tasks:

  - name: Create job to remove old compressed Postgres logfiles in /var/log/postgresql
    cron:
      name: Remove old compressed Postgres logfiles
      user: postgres
      minute: "0"
      hour: "7,19"
      job: "find /var/log/postgresql -type f -name '*.log*.gz' -mtime +99 -delete"

  - name: Delete unnecessary job
    cron:
      name: "Run pg_stat_activity_snapshot.sh"
      user: postgres
      state: absent
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [cron module] **************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Create job to remove old compressed Postgres logfiles in /var/log/postgresql] *********************************
changed: [pg-standalone-01.example.com]

TASK [Delete unnecessary job] ***************************************************************************************
changed: [pg-standalone-01.example.com]

PLAY RECAP **********************************************************************************************************
pg-standalone-01.example.com          : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>

### Module debug

```yaml
---
- name: debug module
  hosts: all
  become: True
  tasks:

  - name: Get Postgres version
    shell: su -l -c "psql -tA -c 'select version()'" postgres | egrep "^PostgreSQL"
    register: pg_version
    changed_when: no

  - name: Example of usage var
    debug:
      var: pg_version

  - name: Example of usage msg
    debug:
      msg: "Current Postgres version: {{ pg_version.stdout }}"
```

<details>
  <summary>Example Output (Click to expand)</summary>

```json
PLAY [debug module] *************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Get Postgres version] *****************************************************************************************
ok: [pg-standalone-01.example.com]

TASK [Example of usage var] *****************************************************************************************
ok: [pg-standalone-01.example.com] => {
    "pg_version": {
        "changed": false,
        "cmd": "su -l -c \"psql -tA -c 'select version()'\" postgres | egrep \"^PostgreSQL\"",
        "delta": "0:00:00.099586",
        "end": "2024-08-01 20:38:17.053961",
        "failed": false,
        "msg": "",
        "rc": 0,
        "start": "2024-08-01 20:38:16.954375",
        "stderr": "",
        "stderr_lines": [],
        "stdout": "PostgreSQL 15.6 (Ubuntu 15.6-1.pgdg22.04+1) on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 11.4.0-1ubuntu1~22.04) 11.4.0, 64-bit",
        "stdout_lines": [
            "PostgreSQL 15.6 (Ubuntu 15.6-1.pgdg22.04+1) on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 11.4.0-1ubuntu1~22.04) 11.4.0, 64-bit"
        ]
    }
}

TASK [Example of usage msg] *****************************************************************************************
ok: [pg-standalone-01.example.com] => {
    "msg": "Current Postgres version: PostgreSQL 15.6 (Ubuntu 15.6-1.pgdg22.04+1) on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 11.4.0-1ubuntu1~22.04) 11.4.0, 64-bit"
}

PLAY RECAP **********************************************************************************************************
pg-standalone-01.example.com          : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

</details>
