=================================================================
na_elementsw_access_group - Manage Element Software Access Groups
================================================================
New in version 2.6

========
Synopsis
========
Create, destroy, or update access groups on Element Software Cluster.

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
| state                |                     | Whether the specified access group       |
|                      |                     | should exist or not                      |
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
| src_access_group_id  |                     | ID or Name of the access group to modify |
|                      |                     | or delete. Required for delete and       |
|                      |                     | modify operations.                       |
+----------------------+---------------------+------------------------------------------+
| new_name             |                     | New name for the access group for create |
|                      |                     | and modify operation. Required for       |
|                      |                     | create operation.                        |
+----------------------+---------------------+------------------------------------------+
| initiators           |                     | List of initiators to include in the     |
|                      |                     | access group. If unspecified, the access |
|                      |                     | group will start out without configured  |
|                      |                     | initiators.                              |
+----------------------+---------------------+------------------------------------------+
| volumes              |                     | List of volumes to initially include in  |
|                      |                     | the volume access group. If unspecified, |
|                      |                     | the access group will start without any  |
|                      |                     | volumes.                                 |
+----------------------+---------------------+------------------------------------------+
| virtual_network_id   |                     | The ID of the Element SW Software        |
|                      |                     | Cluster Virtual Network ID to associate  |
|                      |                     | the access group with.                   |
+----------------------+---------------------+------------------------------------------+
| virtual_network_tags |                     | The ID of the VLAN Virtual Network Tag   |
|                      |                     | to associate the access group with.      |
+----------------------+---------------------+------------------------------------------+
| attributes           |                     | List of Name/Value pairs in JSON object  |
|                      |                     | format.                                  |
+----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

- name: Create Access Group
     na_elementsw_access_group:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: present
       new_name: AnsibleAccessGroup
       volumes: [7,8]

   - name: Modify Access Group
     na_elementsw_access_group:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: present
       src_access_group_id: AnsibleAccessGroup
       new_name: AnsibleAccessGroup-Renamed
       attributes: {"volumes": [1,2,3], "virtual_network_id": 12345}

   - name: Delete Access Group
     na_elementsw_access_group:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: absent
       src_access_group_id: 1
