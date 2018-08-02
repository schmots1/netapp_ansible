=========================================================
na_ontap_volume_clone - Manage NetApp ONTAP volume clones 
=========================================================
New in version 2.5.

========
Synopsis
========
Create, destroy or modify volumes clones on NetApp ONTAP

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
| hostname        |                     | The hostname or IP address of the ONTAP  |
| (required)      |                     | instance.                                |
+-----------------+---------------------+------------------------------------------+
| https           | Default: false      | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| parent_snapshot |                     | Parent snapshot in which volume clone is |
|                 |                     | created off.                             |
+-----------------+---------------------+------------------------------------------+
| parent_volume   |                     | Parent volume of the volume clone being  |
| (required)      |                     | created.                                 |
+-----------------+---------------------+------------------------------------------+
| parent_vserver  |                     | SVM of parent volume in which clone is   |
|                 |                     | created off.                             |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| qos_policy_group|                     | The qos-policy-group-name which should be|
| _name           |                     | set for volume clone.                    |
+-----------------+---------------------+------------------------------------------+
| space_reserve   |                     | FlexVol's space guarantee style. None or |
|                 |                     | volume.                                  |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the specified volume clone should|
|                 |                     | exist or not.                            |
|                 | * present (default) |                                          |
|                 | * absent            |                                          |
+-----------------+---------------------+------------------------------------------+
| volume_type     | Default: RW         | The FlexVol type, either RW or DP        |
+-----------------+---------------------+------------------------------------------+
| username        |                     | This can be a Cluster-scoped or          |
| (required)      |                     | SVM-scoped account, depending on whether |
|                 |                     | a Cluster-level or SVM-level API is      |
|                 |                     | required. For more information, please   |
|                 |                     | read the documentation                   |
|                 |                     | https://goo.gl/BRu78Z.                   |
+-----------------+---------------------+------------------------------------------+
| volume          |                     | The name of the volume clone being       |
| (required)      |                     | created                                  |
+-----------------+---------------------+------------------------------------------+
| vserver         |                     | The SVM to use                           |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: create volume clone
   na_ontap_volume_clone:
     state=present
     username=admin
     password=netapp1!
     hostname=10.193.74.27
     vserver=vs_hack
     parent_volume=normal_volume
     volume=clone_volume_7
     space_reserve=none
     parent_snapshot=backup1
