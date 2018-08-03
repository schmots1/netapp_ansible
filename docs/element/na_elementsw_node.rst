=================================================================
na_elementsw_node - Element Software Node Operation
=================================================================
New in version 2.6

========
Synopsis
========
Manage Element Software Node Operation

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
| state                | Choices:            | Element Software Storage Node operation  |
|                      |                     | state.                                   |
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
| node_id              |                     | List of IDs or Names or IP Address of    |
| (required)           |                     | nodes from cluster used for operation.   |
+----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

   - name: Add node from pending to active cluster
     tags:
     - elementsw_add_node
     na_elementsw_node:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: present
       node_id: sf4805-meg-03

   - name: Remove active node from cluster
     tags:
     - elementsw_remove_node
     na_elementsw_node:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: absent
       node_id: 13

   - name: Add node from pending to active cluster using node IP
     tags:
     - elementsw_add_node_ip
     na_elementsw_node:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: present
       node_id: 10.109.48.65
