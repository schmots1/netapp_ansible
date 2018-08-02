======================================================
na_ontap_net_port - Manage NetApp ONTAP network ports.
======================================================
New in version 2.5.

========
Synopsis
========
Modify a ONTAP network port.

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

+---------------------+---------------------+------------------------------------------+
|   Parameter         |   Choices/Defaults  |                 Comments                 |
+---------------------+---------------------+------------------------------------------+
| autonegotiate_admin |                     | Enables or disables Ethernet auto-       |
|                     |                     | negotiation of speed, duplex and flow    |
|                     |                     | control.                                 |
+---------------------+---------------------+------------------------------------------+
| duplex_admin        |                     | Specifies the user preferred duplex      |
|                     |                     | setting on the port.                     |
+---------------------+---------------------+------------------------------------------+
| flowcontrol_admin   |                     | Specifies the user perferred flow control|
|                     |                     | setting of the port.                     |
+---------------------+---------------------+------------------------------------------+
| hostname            |                     | The hostname or IP address of the ONTAP  |
| (required)          |                     | instance.                                |
+---------------------+---------------------+------------------------------------------+
| https               | Default: false      | Enable and disable https                 |
+---------------------+---------------------+------------------------------------------+
| ipspace             |                     | Specifies the port's associated IPspace  |
|                     |                     | name. Note the 'Cluster' ipspace is      |
|                     |                     | reserved for cluster ports.              |
+---------------------+---------------------+------------------------------------------+
| mtu                 |                     | Specifies the maximum transmission unit  |
|                     |                     | (MTU) reported by the port.              |
+---------------------+---------------------+------------------------------------------+
| node                |                     | Specifies the name of the node.          |
| (required)          |                     |                                          |
+---------------------+---------------------+------------------------------------------+
| password            |                     | Password for the specified user.         |
| (required)          |                     |                                          |
+---------------------+---------------------+------------------------------------------+
| port                |                     | Specifies the name of the port.          | 
| (required)          |                     |                                          |
+---------------------+---------------------+------------------------------------------+
| state               | Choices:            | Whether the specified aggregate should   |
|                     |                     | exist or not.                            |
|                     | * present (default) |                                          |
|                     | * absent            |                                          |
+---------------------+---------------------+------------------------------------------+
| username            |                     | This can be a Cluster-scoped or          |
| (required)          |                     | SVM-scoped account, depending on whether |
|                     |                     | a Cluster-level or SVM-level API is      |
|                     |                     | required. For more information, please   |
|                     |                     | read the documentation                   |
|                     |                     | https://goo.gl/BRu78Z.                   |
+---------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Modify Net Port
   na_ontap_net_port:
     action={{ action }}
     username={{ netapp_username }}
     password={{ netapp_password }}
     hostname={{ netapp_hostname }}
     node={{ Vsim server name }}
     port=e0d
     autonegotiate_admin=true
