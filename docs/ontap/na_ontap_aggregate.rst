====================================================
na_ontap_aggregate - Manage NetApp ONTAP aggregates.
====================================================
New in version 2.6

========
Synopsis
========
Create or destroy aggregates on NetApp ONTAP.

============
Requirements
============
The below requirements are needed on the host that executes this module.

* An ONTAP 9 system. The modules were developed with ONTAP 9.3
* Ansible 2.4 or higher
* netapp-lib (2017.10.30). Install using 'pip install netapp-lib'

==========
Parameters
==========

+-----------------+---------------------+------------------------------------------+
|   Parameter     |   Choices/Defaults  |                 Comments                 |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the specified aggregate should   |
|                 |                     | exist or not.                            |
|                 | * present (default) |                                          |
|                 | * absent            |                                          |
+-----------------+---------------------+------------------------------------------+
| hostname        |                     | The hostname or IP address of the ONTAP  |
| (required)      |                     | instance.                                |
+-----------------+---------------------+------------------------------------------+
| username        |                     | This can be a Cluster-scoped or          |
| (required)      |                     | SVM-scoped account, depending on whether |
|                 |                     | a Cluster-level or SVM-level API is      |
|                 |                     | required. For more information, please   |
|                 |                     | read the documentation                   |
|                 |                     | https://goo.gl/BRu78Z.                   |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| https           | Default: false      | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| no_cert_verify  | Default: false      | Set to true in order to use self-signed  |
|                 |                     | certificates with https.  *Warning: this |
|                 |                     | does open up the small possiblity of a   |
|                 |                     | man-in-the-middle attack.                |
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
| disk_size       |                     | Disk size to use in 4K block size.       |
|                 |                     | Disks within 10% of specified size will  |
|                 |                     | be used.                                 |
+-----------------+---------------------+------------------------------------------+
| disk_type       | Choices:            | Type of disk to use to build aggregate.  |
|                 |                     |                                          |
|                 | * ATA               |                                          |
|                 | * BSAS              |                                          |
|                 | * FCAL              |                                          |
|                 | * FSAS              |                                          |
|                 | * LUN               |                                          |
|                 | * MSATA             |                                          |
|                 | * SAS               |                                          |
|                 | * SSD               |                                          |
|                 | * VMDISK            |                                          |
+-----------------+---------------------+------------------------------------------+
| raid_size       |                     | Sets the maximum number of drives per    |
|                 |                     | raid group.                              |
+-----------------+---------------------+------------------------------------------+
| raid_type       |                     | Specifies the type of RAID groups to use |
|                 |                     | in the new aggregate.                    |
+-----------------+---------------------+------------------------------------------+
| from_name       |                     | Name of aggregate to be renamed.         |
|                 |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| name            |                     | The name of the aggregate to manage.     |
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
| nodes           |                     | Node that aggregate should be created on |
|                 |                     | or Nodes it should stripe across.        |
+-----------------+---------------------+------------------------------------------+
| unmount_volumes | Choices:            | If set to "TRUE", this option specifies  |
|                 |                     | that all of the volumes hosted by the    |
|                 | * true              | given aggregate are to be unmounted      |
|                 | * false             | before the offline operation is executed.|
|                 |                     | By default, the system will reject any   |
|                 |                     | attempt to offline an aggregate that     | 
|                 |                     | hosts one or more online volumes.        |
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

