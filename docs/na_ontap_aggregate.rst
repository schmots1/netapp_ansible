====================================================
na_ontap_aggregate - Manage NetApp Ontap aggregates.
====================================================
New in version 2.5.

========
Synopsis
========
Create or destroy aggregates on NetApp cDOT.

============
Requirements
============
The below requirements are needed on the host that executes this module.

* A Data ONTAP system. The modules were developed with Clustered Data ONTAP 9.3
* Ansible 2.4
* netapp-lib (2017.10.30). Install using ‘pip install netapp-lib’

==========
Parameters
==========

+-----------------+---------------------+------------------------------------------+
|   Parameter     |   Choices/Defaults  |                 Comments                 |
+-----------------+---------------------+------------------------------------------+
| disk_count      |                     | Number of disks to place into the        |
|                 |                     | aggregate, including parity disks.  The  |
|                 |                     | disks in this newly-created aggregate    |
|                 |                     | come from the spare disk pool. The       |
|                 |                     | smallest disks in this pool join the     |
|                 |                     | aggregate first, unless the disk-size    |
|                 |                     | argument is provided. Either disk-count  | 
|                 |                     | or disks must be supplied.               |
|                 |                     | Range [0..2^31-1].  Required when        |
|                 |                     | state=present.                           |
+-----------------+---------------------+------------------------------------------+
| hostname        |                     | The hostname or IP address of the ONTAP  |
| (required)      |                     | instance.                                |
+-----------------+---------------------+------------------------------------------+
| https           | Default: no         | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| name            |                     | The name of the aggregate to manage.     |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| rename          |                     | The name of the aggregate that replaces  |
|                 |                     | the current name.                        |
+-----------------+---------------------+------------------------------------------+
| service_state   | Choices:            | Whether the specified aggregate should be|
|                 |                     | enabled or disabled. Creates aggregate if|
|                 | * online            | it doesn't exist.                        |
|                 | * offline           |                                          |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the specified aggregate should   |
|                 |                     | exist or not.                            |
|                 | * present (default) |                                          |
|                 | * absent            |                                          |
+-----------------+---------------------+------------------------------------------+
| unmount_volumes | Choices:            | If set to "TRUE", this option specifies  |
|                 |                     | that all of the volumes hosted by the    |
|                 | * true              | given aggregate are to be unmounted      |
|                 | * false             | before the offline operation is executed.|
|                 |                     | By default, the system will reject any   |
|                 |                     | attempt to offline an aggregate that     | 
|                 |                     | hosts one or more online volumes.        |
+-----------------+---------------------+------------------------------------------+
| username        |                     | This can be a Cluster-scoped or          |
| (required)      |                     | SVM-scoped account, depending on whether |
|                 |                     | a Cluster-level or SVM-level API is      |
|                 |                     | required. For more information, please   |
|                 |                     | read the documentation                   |
|                 |                     | https://goo.gl/BRu78Z.                   |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create Aggregates
   na_ontap_aggregate:
     state: present
     service_state: online
     name: ansibleAggr
     disk_count: 1
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: Manage Aggregates
   na_ontap_aggregate:
     state: present
     service_state: offline
     unmount_volumes: true
     name: ansibleAggr
     disk_count: 1
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: Rename Aggregates
   na_ontap_aggregate:
     state: present
     service_state: online
     name: ansibleAggr
     rename: ansibleAggr2
     disk_count: 1
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: Delete Aggregates
   na_ontap_aggregate:
     state: absent
     service_state: offline
     unmount_volumes: true
     name: ansibleAggr
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

