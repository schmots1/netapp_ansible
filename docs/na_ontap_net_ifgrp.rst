====================================================
na_ontap_net_ifgrp - Manage NetApp Ontap interface groups.
====================================================
New in version 2.5.

========
Synopsis
========
Create, modify or destroy the network interface group.

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

+-----------------------+---------------------+------------------------------------------+
|   Parameter           |   Choices/Defaults  |                 Comments                 |
+-----------------------+---------------------+------------------------------------------+
| distribution_function |                     | Specifies the traffic distribution       |
|                       |                     | function for the ifgrp.                  |
+-----------------------+---------------------+------------------------------------------+
| hostname              |                     | The hostname or IP address of the ONTAP  |
| (required)            |                     | instance.                                |
+-----------------------+---------------------+------------------------------------------+
| https                 | Default: false      | Enable and disable https                 |
+-----------------------+---------------------+------------------------------------------+
| mode                  |                     | Specifies the link policy for the ifgrp  |
+-----------------------+---------------------+------------------------------------------+
| name                  |                     | The name of the interface group to manage|
| (required)            |                     |                                          |
+-----------------------+---------------------+------------------------------------------+
| node                  |                     | Specifies the name of the node.          |
| (required)            |                     |                                          |
+-----------------------+---------------------+------------------------------------------+
| password              |                     | Password for the specified user.         |
| (required)            |                     |                                          |
+-----------------------+---------------------+------------------------------------------+
| port                  |                     | Adds the specified port.                 |
+-----------------------+---------------------+------------------------------------------+
| state                 | Choices:            | Whether the specified aggregate should   |
|                       |                     | exist or not.                            |
|                       | * present (default) |                                          |
|                       | * absent            |                                          |
+-----------------------+---------------------+------------------------------------------+
| username              |                     | This can be a Cluster-scoped or          |
| (required)            |                     | SVM-scoped account, depending on whether |
|                       |                     | a Cluster-level or SVM-level API is      |
|                       |                     | required. For more information, please   |
|                       |                     | read the documentation                   |
|                       |                     | https://goo.gl/BRu78Z.                   |
+-----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: create ifgrp
   na_ontap_net_ifgrp:
     state=present
     username={{ netapp_username }}
     password={{ netapp_password }}
     hostname={{ netapp_hostname }}
     distribution_function=ip
     name=a0c
     port=e0d
     mode=multimode
     node={{ Vsim node name }}
 - name: delete ifgrp
   na_ontap_net_ifgrp:
     state=absent
     username={{ netapp_username }}
     password={{ netapp_password }}
     hostname={{ netapp_hostname }}
     name=a0c
     node={{ Vsim node name }}
