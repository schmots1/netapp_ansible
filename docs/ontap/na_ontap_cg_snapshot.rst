======================================================================
na_ontap_cg_snapshot - Manage NetApp ONTAP Consistancy Group Snapshots
======================================================================
New in version 2.7

========
Synopsis
========
Create consistancy group snapshot for ONTAP volumes.

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

+------------------+---------------------+------------------------------------------+
|   Parameter      |   Choices/Defaults  |                 Comments                 |
+------------------+---------------------+------------------------------------------+
| state            | Choices:            | If you want to create a snapshot.        |
|                  |                     |                                          |
|                  | * present (default) |                                          |
|                  | * absent            |                                          |
+------------------+---------------------+------------------------------------------+
| hostname         |                     | The hostname or IP address of the ONTAP  |
| (required)       |                     | instance.                                |
+------------------+---------------------+------------------------------------------+
| username         |                     | This can be a Cluster-scoped or          |
| (required)       |                     | SVM-scoped account, depending on whether |
|                  |                     | a Cluster-level or SVM-level API is      |
|                  |                     | required. For more information, please   |
|                  |                     | read the documentation                   |
|                  |                     | https://goo.gl/BRu78Z.                   |
+------------------+---------------------+------------------------------------------+
| password         |                     | Password for the specified user.         |
| (required)       |                     |                                          |
+------------------+---------------------+------------------------------------------+
| https            | Default: false      | Enable and disable https                 |
+------------------+---------------------+------------------------------------------+
| validate_certs   | Default: true       | Set to false in order to use self-signed |
|                  |                     | certificates with https.  *Warning: this |
|                  |                     | does open up the small possiblity of a   |
|                  |                     | man-in-the-middle attack.                |
+------------------+---------------------+------------------------------------------+
| snapmirrot_label |                     | A human readable SnapMirror label to be  |
|                  |                     | attached with the consistency group      |
|                  |                     | snapshot copies.                         |
+------------------+---------------------+------------------------------------------+
| snapshot         |                     | The provided name of the snapshot that   |
|                  |                     | is created in each volume.               |
+------------------+---------------------+------------------------------------------+
| timeout          | Choices:            | Timeout Selector                         |
|                  |                     |                                          |
|                  | * urgant            |                                          |
|                  | * medium            |                                          |
|                  | * relaxed           |                                          |
|                  |                     |                                          |
|                  | Default: medium     |                                          |
+------------------+---------------------+------------------------------------------+
| volumes          |                     | A list of volumes in this filer that is  |
|                  |                     | part of this CG operation.               |
+------------------+---------------------+------------------------------------------+
| vserver          |                     | Name of Storage Virtual Machine.         |
+------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

- name:
      na_ontap_cg_snapshot:
        state: present
        vserver: vserver_name
        snapshot: snapshot name
        volume: vol_name
        username: "{{ netapp username }}"
        password: "{{ netapp password }}"
        hostname: "{{ netapp hostname }}"
