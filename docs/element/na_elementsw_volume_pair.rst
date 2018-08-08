=================================================================
na_elementsw_volume_pair - Manage Element Software Volume Pair
=================================================================
New in version 2.6

========
Synopsis
========
Create, delete volume pair

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
| state                | Choices:            | Whether the specified volume pair should |
|                      |                     | exist or not.                            |
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
| src_volume           |                     | Source volume name or volume ID          |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| src_account          |                     | Source account name or volume ID         |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| dest_volume          |                     | Destination volume name or volume ID     |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| dest_account         |                     | Destination account name or volume ID    |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| dest_mvip            |                     | Destination IP address of the paired     |
| (required)           |                     | cluster.                                 |
+----------------------+---------------------+------------------------------------------+
| dest_username        |                     | Destination username of the paired       |
|                      |                     | cluster. Optional if this is same as     |
|                      |                     | source cluster username.                 |
+----------------------+---------------------+------------------------------------------+
| dest_password        |                     | Destination password of the paired       |
|                      |                     | cluster. Optional if this is same as     |
|                      |                     | source cluster password.                 |
+----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

   - name: Create volume pair
     na_elementsw_volume_pair:
       hostname: "{{ src_cluster_hostname }}"
       username: "{{ src_cluster_username }}"
       password: "{{ src_cluster_password }}"
       state: present
       src_volume: test1
       src_account: test2
       dest_volume: test3
       dest_account: test4
       mode: sync
       dest_mvip: "{{ dest_cluster_hostname }}"

   - name: Delete volume pair
     na_elementsw_volume_pair:
       hostname: "{{ src_cluster_hostname }}"
       username: "{{ src_cluster_username }}"
       password: "{{ src_cluster_password }}"
       state: absent
       src_volume: 3
       src_account: 1
       dest_volume: 2
       dest_account: 1
       dest_mvip: "{{ dest_cluster_hostname }}"
       dest_username: "{{ dest_cluster_username }}"
       dest_password: "{{ dest_cluster_password }}"
