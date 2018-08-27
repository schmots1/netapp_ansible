======================================================
na_ontap_net_vlan - Manage NetApp ONTAP network vlans.
======================================================
New in version 2.5.

========
Synopsis
========
Create or delete network vlans

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
| validate_certs  | Default: true       | Set to false in order to use self-signed |
|                 |                     | certificates with https.  *Warning: this |
|                 |                     | does open up the small possiblity of a   |
|                 |                     | man-in-the-middle attack.                |
+-----------------+---------------------+------------------------------------------+
| interface_name  |                     | Name of the vlan interface.  The name    |
|                 |                     | must be of the format                    |
|                 |                     | <parent-interface>-<vlanid>              |
+-----------------+---------------------+------------------------------------------+
| node            |                     | Node name of vlan interface.             |
+-----------------+---------------------+------------------------------------------+
| parent_interface|                     | The interface that hosts the vlan        |
| (required)      |                     | interface                                |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the specified aggregate should   |
|                 |                     | exist or not.                            |
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
| vlanid          |                     | The vlan id. Range 1..4094               |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: create vlan
   na_ontap_net_vlan:
     state=present
     vlanid=13
     node={{ vlan node }}
     parent_interface={{ vlan parent interface name }}
     username={{ netapp_username }}
     password={{ netapp_password }}
     hostname={{ netapp_hostname }}
