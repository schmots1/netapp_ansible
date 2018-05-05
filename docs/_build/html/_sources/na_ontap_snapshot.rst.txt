====================================================
na_ontap_snapshot - Manage NetApp ONTAP Snapshots 
====================================================
New in version 2.5.

========
Synopsis
========
Create, modify, or delete ONTAP Snapshots

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

+------------------------+---------------------+------------------------------------------+
|   Parameter            |   Choices/Defaults  |                 Comments                 |
+------------------------+---------------------+------------------------------------------+
| async                  |                     | If true, the snapshot is to be create    | 
|                        |                     | asynchronously.                          |
+------------------------+---------------------+------------------------------------------+
| comment                |                     | A human readable comment attached with   |
|                        |                     | the Snapshot.  The size of the comment   |
|                        |                     | can be at most 255 characters.           |
+------------------------+---------------------+------------------------------------------+
| hostname               |                     | The hostname or IP address of the ONTAP  |
| (required)             |                     | instance.                                |
+------------------------+---------------------+------------------------------------------+
| https                  | Default: false      | Enable and disable https                 |
+------------------------+---------------------+------------------------------------------+
| ignore_owners          |                     | If this field is true, Snapshot will be  | 
|                        |                     | deleted even if some other processes are |
|                        |                     | accessing it.                            |
+------------------------+---------------------+------------------------------------------+
| new_comment            |                     | A human readable comment attached with   |
|                        |                     | the Snapshot.  The size of the comment   |
|                        |                     | can be at most 255 characters. This will |
|                        |                     | replace the existing comment.            |
+------------------------+---------------------+------------------------------------------+
| password               |                     | Password for the specified user.         |
| (required)             |                     |                                          |
+------------------------+---------------------+------------------------------------------+
| snapmirror_label       |                     | A human readable SnapMirror Label        |
|                        |                     | attached with the snapshot. Size of the  |
|                        |                     | label can be at most 31 characters.      |
+------------------------+---------------------+------------------------------------------+
| snapshot               |                     | Name of the snapshot to be created. The  |
|                        |                     | maximum string length is 256 characters. |
+------------------------+---------------------+------------------------------------------+
| snapshot_instance_uuid |                     | The 128 bit unique snapshot identifier   |
|                        |                     | expressed in the form of UUID.           |
+------------------------+---------------------+------------------------------------------+
| state                  | Choices:            | Whether the specified aggregate should   |
|                        |                     | exist or not.                            |
|                        | * present (default) |                                          |
|                        | * absent            |                                          |
+------------------------+---------------------+------------------------------------------+
| username               |                     | This can be a Cluster-scoped or          |
| (required)             |                     | SVM-scoped account, depending on whether |
|                        |                     | a Cluster-level or SVM-level API is      |
|                        |                     | required. For more information, please   |
|                        |                     | read the documentation                   |
|                        |                     | https://goo.gl/BRu78Z.                   |
+------------------------+---------------------+------------------------------------------+
| volume                 |                     | Name of the FlexVol on which the snapshot|
| (required)             |                     | is to be created.                        |
+------------------------+---------------------+------------------------------------------+
| vserver                |                     | The SVM name where the Snapshot will be  |
+------------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: create SnapShot
   tags:
     - create
   na_ontap_snapshot:
     state=present
     snapshot={{ snapshot name }}
     volume={{ vol name }}
     comment="i am a comment"
     vserver={{ vserver name }}
     username={{ netapp username }}
     password={{ netapp password }}
     hostname={{ netapp hostname }}
 
 - name: delete SnapShot
   tags:
     - delete
   na_ontap_snapshot:
     state=absent
     snapshot={{ snapshot name }}
     volume={{ vol name }}
     vserver={{ vserver name }}
     username={{ netapp username }}
     password={{ netapp password }}
     hostname={{ netapp hostname }}
 
 - name: modify SnapShot
   tags:
     - modify
   na_ontap_snapshot:
     state=present
     snapshot={{ snapshot name }}
     new_comment="New comments are great"
     volume={{ vol name }}
     vserver={{ vserver name }}
     username={{ netapp username }}
     password={{ netapp password }}
     hostname={{ netapp hostname }}

