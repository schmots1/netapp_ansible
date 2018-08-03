=================================================================
na_elementsw_cluster_pair - Manage Element Software Cluster Pair
=================================================================
New in version 2.6

========
Synopsis
========
Create, delete cluster pair

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
| state                | Choices:            | Whether the specified cluster pair       |
|                      |                     | should exist or not                      |
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
| dest_hostname        |                     | Destination IP address of the cluster to |
| (required)           |                     | be paired.                               |
+----------------------+---------------------+------------------------------------------+
| dest_username        |                     | Destination username for the cluster to  |
|                      |                     | be paired.Optional if this is same as    |
|                      |                     | source cluster username.                 |
+----------------------+---------------------+------------------------------------------+
| dest_password        |                     | Destination password for the cluster to  |
|                      |                     | be paired.Optional if this is same as    |
|                      |                     | source cluster password.                 |
+----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

   - name: Create cluster pair
     na_elementsw_cluster_pair:
       hostname: "{{ src_hostname }}"
       username: "{{ src_username }}"
       password: "{{ src_password }}"
       state: present
       dest_mvip: "{{ dest_hostname }}"

   - name: Delete cluster pair
     na_elementsw_cluster_pair:
       hostname: "{{ src_hostname }}"
       username: "{{ src_username }}"
       password: "{{ src_password }}"
       state: absent
       ddest_mvip: "{{ dest_hostname }}"
       dest_username: "{{ dest_username }}"
       dest_password: "{{ dest_password }}"
