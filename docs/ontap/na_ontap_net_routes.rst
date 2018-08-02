====================================================
na_ontap_net_routes - Manage NetApp Ontap network routes.
====================================================
New in version 2.5.

========
Synopsis
========
Modify ONTAP network routes

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
| destination     |                     | Specify the route destination. Example   |
| (required)      |                     | 10.7.125.5/20, fd20:13::/64              |
+-----------------+---------------------+------------------------------------------+
| gateway         |                     | Specify the route gateway. Example       |
| (required)      |                     | 10.7.125.1,fd20:13::1                    |
+-----------------+---------------------+------------------------------------------+
| hostname        |                     | The hostname or IP address of the ONTAP  |
| (required)      |                     | instance.                                |
+-----------------+---------------------+------------------------------------------+
| https           | Default: false      | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| metric          |                     | Specify the route metric. If this field  |
|                 |                     | is not provided the default will be set  |
|                 |                     | to 30                                    |
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
| vserver         |                     | The name of the SVM                      |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: create route
   na_ontap_net_routes:
     action={{ action }}
     vserver={{ Vserver name }}
     username={{ netapp_username }}
     password={{ netapp_password }}
     hostname={{ netapp_hostname }}
     destination=10.7.125.5/20
     gateway=10.7.125.1
     metric=30
