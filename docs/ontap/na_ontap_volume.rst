====================================================
na_ontap_volume - Manage NetApp Ontap volumes 
====================================================
New in version 2.5.

========
Synopsis
========
Create, destroy or modify volumes on NetApp ONTAP

============
Requirements
============
The below requirements are needed on the host that executes this module.

* A Data ONTAP system. The modules were developed with Clustered Data ONTAP 9.3
* Ansible 2.4
* netapp-lib (2017.10.30). Install using 'pip install netapp-lib'

==========
Parameters
==========

+-----------------+---------------------+------------------------------------------+
|   Parameter     |   Choices/Defaults  |                 Comments                 |
+-----------------+---------------------+------------------------------------------+
| aggregate_name  |                     | The name of the aggregate the FlexVol    |
|                 |                     | should exist on.  Required when          |
|                 |                     | state=present.                           |
+-----------------+---------------------+------------------------------------------+
| hostname        |                     | The hostname or IP address of the ONTAP  |
| (required)      |                     | instance.                                |
+-----------------+---------------------+------------------------------------------+
| https           | Default: false      | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| infinate        | True/False(Default) | Set True if the volume is an Infinite Vol|
+-----------------+---------------------+------------------------------------------+
| junction_path   |                     | FlexVol's junction path                  |
+-----------------+---------------------+------------------------------------------+
| name            |                     | The name of the FlexVol to manage.       |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| new_name        |                     | New name of FlexVol to be renamed        | 
+-----------------+---------------------+------------------------------------------+
| online          | True(Default)/False | Whether the specified FlexVol is online, |
|                 |                     | or not.                                  |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| percent_snapshot|                     | Amount of space reserved for snapshot    |
| _space          |                     | copies of the FlexVol                    |
+-----------------+---------------------+------------------------------------------+
| policy          |                     | Export Policy for FlexVol to use         |
+-----------------+---------------------+------------------------------------------+
| size            |                     | The size of the FlexVol in (size_unit).  |
|                 |                     | Required when state=present              |
+-----------------+---------------------+------------------------------------------+
| size_unit       | Choices:            | The unit used to interpret the size      |
|                 |                     | parameter.                               |
|                 | * bytes             |                                          |
|                 | * b                 |                                          |
|                 | * kb                |                                          |
|                 | * mb                |                                          |
|                 | * gb (Default)      |                                          |
|                 | * tb                |                                          |
|                 | * pb                |                                          |
|                 | * eb                |                                          |
|                 | * zb                |                                          |
|                 | * yb                |                                          |
+-----------------+---------------------+------------------------------------------+
| space_guarantee |                     | FlexVol's space guarantee style. None or |
|                 |                     | volume.                                  |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the specified FlexVol should     |
|                 |                     | exist or not.                            |
|                 | * present (default) |                                          |
|                 | * absent            |                                          |
+-----------------+---------------------+------------------------------------------+
| type            | Default: RW         | The FlexVol type, either RW or DP        |
+-----------------+---------------------+------------------------------------------+
| username        |                     | This can be a Cluster-scoped or          |
| (required)      |                     | SVM-scoped account, depending on whether |
|                 |                     | a Cluster-level or SVM-level API is      |
|                 |                     | required. For more information, please   |
|                 |                     | read the documentation                   |
|                 |                     | https://goo.gl/BRu78Z.                   |
+-----------------+---------------------+------------------------------------------+
| volume_security_| Choices:            | The security style associated with this  |
| style           |                     | FlexVol                                  |
|                 | * mixed (Default)   |                                          |
|                 | * ntfs              |                                          |
|                 | * unified           |                                          |
|                 | * unix              |                                          |
+-----------------+---------------------+------------------------------------------+
| vserver         |                     | The SVM to use                           |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create FlexVol
   na_ontap_volume:
     state: present
     name: ansibleVolume
     infinite: False
     aggregate_name: aggr1
     size: 20
     size_unit: mb
     junction_path: /ansibleVolume11
     vserver: ansibleVServer
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: Make FlexVol offline
   na_ontap_volume:
     state: present
     name: ansibleVolume
     infinite: False
     online: False
     vserver: ansibleVServer
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
