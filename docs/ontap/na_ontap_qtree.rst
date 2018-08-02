====================================================
na_ontap_qtree - Manage NetApp ONTAP Qtrees.
====================================================
New in version 2.5.

========
Synopsis
========
Create or destroy Qtrees on NetApp ONTAP.

============
Requirements
============
The below requirements are needed on the host that executes this module.

* An ONTAP system. The modules were developed with ONTAP 9.3
* Ansible 2.4 or higher
* netapp-lib (2017.10.30). Install using 'pip install netapp-lib'

==========
Parameters
==========

+-----------------+---------------------+------------------------------------------+
|   Parameter     |   Choices/Defaults  |                 Comments                 |
+-----------------+---------------------+------------------------------------------+
| flexvol_name    |                     | The name of the FlexVol the Qtree should |
|                 |                     | exist on.  Required when state=present   |
+-----------------+---------------------+------------------------------------------+
| hostname        |                     | The hostname or IP address of the ONTAP  |
| (required)      |                     | instance.                                |
+-----------------+---------------------+------------------------------------------+
| https           | Default: false      | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| name            |                     | The name of the Qtree to manage.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the specified Qtree should exist |
|                 |                     | or not.                                  |
|                 | * present (default) |                                          |
|                 | * absent            |                                          |
+-----------------+---------------------+------------------------------------------+
| username        |                     | This can be a Cluster-scoped or          |
| (required)      |                     | SVM-scoped account, depending on whether |
|                 |                     | a Cluster-level or SVM-level API is      |
|                 |                     | required. For more information, please   |
|                 |                     | read the documentation                   |
|                 |                     | https://goo.gl/BRu78Z.                   |
+-----------------+---------------------+------------------------------------------+
| vserver         |                     | The name of the SVM to use               |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create QTree
   na_ontap_qtree:
     state: present
     name: ansibleQTree
     flexvol_name: ansibleVolume
     vserver: ansibleVServer
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: Delete QTree
   na_ontap_qtree:
     state: absent
     name: ansibleQTree
     flexvol_name: ansibleVolume
     vserver: ansibleVServer
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

