=============================================================================
na_ontap_broadcast_domain_ports - Manage NetApp ONTAP broadcast domain ports.
=============================================================================
New in version 2.5.

========
Synopsis
========
Modify an ONTAP broacast domain ports.

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
| state            | Choices:            | Whether the specified broadcast domain   |
|                  |                     | should exist or not.                     |
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
| broadcast_domain |                     | Specify the broadcast domain name        |
| (required)       |                     |                                          |
+------------------+---------------------+------------------------------------------+
| ipspace          |                     | Specify the required ipspace for the     |
|                  |                     | broadcast domain                         |
+------------------+---------------------+------------------------------------------+
| ports            |                     | Specify the ports associated with this   |
|                  |                     | broadcast domain.  Should be comma       |
|                  |                     | separated.                               |
+------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: create broadcast domain ports
   na_ontap_broadcast_domain_ports:
     state=present
     vserver={{ Vserver name }}
     username={{ netapp_username }}
     password={{ netapp_password }}
     hostname={{ netapp_hostname }}
     broadcast_domain=123kevin
     ports=khutton-vsim1:e0d-13
 - name: delete broadcast domain ports
   na_ontap_broadcast_domain_ports:
     state=absent
     vserver={{ Vserver name }}
     username={{ netapp_username }}
     password={{ netapp_password }}
     hostname={{ netapp_hostname }}
     broadcast_domain=123kevin
     ports=khutton-vsim1:e0d-13
