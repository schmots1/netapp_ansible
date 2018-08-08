================================================
na_elementsw_vlan - Manage Element Software VLAN
================================================
New in version 2.6

========
Synopsis
========
Create, delete, modify VLAN

============
Requirements
============
The below requirements are needed on the host that executes this module.

* An Element software system.  Tested with Element OS 10
* Ansible 2.4 or higher
* solidfire-sdk-python (1.5.0.87). Install using 'pip install solidfire-sdk-python'

==========
Parameters
==========

+----------------------+---------------------+------------------------------------------+
|     Parameter        |   Choices/Defaults  |                 Comments                 |
+----------------------+---------------------+------------------------------------------+
| state                | Choices:            | Whether the specified vlan should exist  |
|                      |                     | or not.                                  |
|                      | * present           |                                          |
|                      | * absent            |                                          |
+----------------------+---------------------+------------------------------------------+
| hostname             |                     | The hostname or IP address of the        |
| (required)           |                     | cluster mvip.                            |
+----------------------+---------------------+------------------------------------------+
| username             |                     | Admin account username.                  |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| password             |                     | Password for the specified username.     |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| vlan_tag             |                     | Virtual Network Tag                      |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| name                 |                     | User defined name for the new VLAN. Name |
|                      |                     | of the vlan is unique. Required for      |
|                      |                     | create.                                  |
+----------------------+---------------------+------------------------------------------+
| svip                 |                     | Storage virtual IP which is unique.      |
|                      |                     | Required for create.                     |
+----------------------+---------------------+------------------------------------------+
| address_blocks       |                     | List of address blocks for the VLAN.     |
|                      |                     | Each address block contains the starting |
|                      |                     | IP address and size for the block.       |
|                      |                     | Required for create.                     |
+----------------------+---------------------+------------------------------------------+
| netmask              |                     | Netmask for the VLAN. Required for       |
|                      |                     | create.                                  |
+----------------------+---------------------+------------------------------------------+
| gateway              |                     | Gateway for the VLAN.                    |
+----------------------+---------------------+------------------------------------------+
| namespace            |                     | Enable or disable namespaces.            |
+----------------------+---------------------+------------------------------------------+
| attributes           |                     | List of Name/Value pairs in JSON object  |
|                      |                     | format.                                  |
+----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

- name: Create vlan
  na_elementsw_vlan:
    state: present
    name: test
    vlan_tag: 1
    svip: "{{ ip address }}"
    netmask: "{{ netmask }}"
    address_blocks:
      - start: "{{ starting ip_address }}"
        size: 5
      - start: "{{ starting ip_address }}"
        size: 5
    hostname: "{{ netapp_hostname }}"
    username: "{{ netapp_username }}"
    password: "{{ netapp_password }}"

- name: Delete Lun
  na_elementsw_vlan:
    state: present
    vlan_tag: 1
    hostname: "{{ netapp_hostname }}"
    username: "{{ netapp_username }}"
    password: "{{ netapp_password }}"
