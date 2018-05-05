==================================================================
na_ontap_broadcast_domain - Manage NetApp Ontap broadcast domains.
==================================================================
New in version 2.5.

========
Synopsis
========
Modify an ONTAP broacast domain.

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

+------------------+---------------------+------------------------------------------+
|   Parameter      |   Choices/Defaults  |                 Comments                 |
+------------------+---------------------+------------------------------------------+
| broadcast_domain |                     | Specify the broadcast domain name        |
| (required)       |                     |                                          |
+------------------+---------------------+------------------------------------------+
| hostname         |                     | The hostname or IP address of the ONTAP  |
| (required)       |                     | instance.                                |
+------------------+---------------------+------------------------------------------+
| https            | Default: false      | Enable and disable https                 |
+------------------+---------------------+------------------------------------------+
| ipspace          |                     | Specify the required ipspace for the     |
|                  |                     | broadcast domain                         |
+------------------+---------------------+------------------------------------------+
| mtu              |                     | Specify the required mtu for the         |
|                  |                     | broadcast domain                         |
+------------------+---------------------+------------------------------------------+
| password         |                     | Password for the specified user.         |
| (required)       |                     |                                          |
+------------------+---------------------+------------------------------------------+
| ports            |                     | Specify the ports associated with this   |
|                  |                     | broadcast domain.  Should be comma       |
|                  |                     | separated.                               |
+------------------+---------------------+------------------------------------------+
| state            | Choices:            | Whether the specified broadcast domain   |
|                  |                     | should exist or not.                     |
|                  | * present (default) |                                          |
|                  | * absent            |                                          |
+------------------+---------------------+------------------------------------------+
| username         |                     | This can be a Cluster-scoped or          |
| (required)       |                     | SVM-scoped account, depending on whether |
|                  |                     | a Cluster-level or SVM-level API is      |
|                  |                     | required. For more information, please   |
|                  |                     | read the documentation                   |
|                  |                     | https://goo.gl/BRu78Z.                   |
+------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: create broadcast domain
   na_ontap_broadcast_domain:
     state=present
     username={{ netapp_username }}
     password={{ netapp_password }}
     hostname={{ netapp_hostname }}
     broadcast_domain=123kevin
     mtu=1000
     ipspace=Default
     ports=khutton-vsim1:e0d-12,khutton-vsim1:e0d-13
 - name: delete broadcast domain
   na_ontap_broadcast_domain:
     state=absent
     username={{ netapp_username }}
     password={{ netapp_password }}
     hostname={{ netapp_hostname }}
     broadcast_domain=123kevin
     mtu=1000
     ipspace=Default
 - name: modify broadcast domain
   na_ontap_broadcast_domain:
     state=modify
     username={{ netapp_username }}
     password={{ netapp_password }}
     hostname={{ netapp_hostname }}
     broadcast_domain=123kevin
     mtu=1100
     ipspace=Default
