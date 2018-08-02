====================================================================================
na_ontap_service_processor_network - Manage NetApp ONTAP service processor networks.
====================================================================================
New in version 2.5.

========
Synopsis
========
Modify a ONTAP serivce processor network

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

+--------------------+---------------------+------------------------------------------+
|   Parameter        |   Choices/Defaults  |                 Comments                 |
+--------------------+---------------------+------------------------------------------+
| address_type       |                     | Specify address class (ipV4 or ipV6)     |
| (required)         |                     |                                          |
+--------------------+---------------------+------------------------------------------+
| dhcp               |                     | Specify dhcp type (v4 or none)           |
+--------------------+---------------------+------------------------------------------+
| gateway_ip_address |                     | Specify the gateway IP address           |
+--------------------+---------------------+------------------------------------------+
| hostname           |                     | The hostname or IP address of the ONTAP  |
| (required)         |                     | instance.                                |
+--------------------+---------------------+------------------------------------------+
| https              | Default: false      | Enable and disable https                 |
+--------------------+---------------------+------------------------------------------+
| ip_address         |                     | Specify the service processor ip address |
+--------------------+---------------------+------------------------------------------+
| is_enabled         |                     | Specify whether to enable or disable the |
| (required)         |                     | service processor network (true or false)|
+--------------------+---------------------+------------------------------------------+
| netmask            |                     | Specify the serivce processor netmask    |
+--------------------+---------------------+------------------------------------------+
| node               |                     | The node where the service processor     |
| (required)         |                     | network should be enabled                |
+--------------------+---------------------+------------------------------------------+
| password           |                     | Password for the specified user.         |
| (required)         |                     |                                          |
+--------------------+---------------------+------------------------------------------+
| prefix_length      |                     | Specify the serivce processor            |
|                    |                     |  prefix_length                           |
+--------------------+---------------------+------------------------------------------+
| username           |                     | This can be a Cluster-scoped or          |
| (required)         |                     | SVM-scoped account, depending on whether |
|                    |                     | a Cluster-level or SVM-level API is      |
|                    |                     | required. For more information, please   |
|                    |                     | read the documentation                   |
|                    |                     | https://goo.gl/BRu78Z.                   |
+--------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Modify Service Processor Network
   na_ontap_service_processor_network:
     state=present
     address_type=ipv4
     is_enabled=true
     dhcp=v4
     node=FPaaS-A300-01
     node={{ netapp_node }}
     username={{ netapp_username }}
     password={{ netapp_password }}
     hostname={{ netapp_hostname }}
