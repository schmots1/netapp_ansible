====================================================
na_ontap_user_role - Manage NetApp Ontap roles.
====================================================
New in version 2.5.

========
Synopsis
========
Create or destory user roles

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
| access_level           | Choices:            | The access level of the role by command  |
|                        |                     |                                          |
|                        | * none              |                                          |
|                        | * readonly          |                                          |
|                        | * all (Default)     |                                          |
+------------------------+---------------------+------------------------------------------+
| command_directory_name |                     | The command or command directory to which|
| (requried)             |                     |  the role has an access                  |
+------------------------+---------------------+------------------------------------------+
| hostname               |                     | The hostname or IP address of the ONTAP  |
| (required)             |                     | instance.                                |
+------------------------+---------------------+------------------------------------------+
| https                  | Default: false      | Enable and disable https                 |
+------------------------+---------------------+------------------------------------------+
| name                   |                     | The name of the role to manage.          |
| (required)             |                     |                                          |
+------------------------+---------------------+------------------------------------------+
| password               |                     | Password for the specified user.         |
| (required)             |                     |                                          |
+------------------------+---------------------+------------------------------------------+
| state                  | Choices:            | Whether the specified role should        |
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
| vserver                |                     | The name of the SVM to use               |
+------------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create User Role
   na_ontap_user_role:
     state: present
     name: ansibleRole
     command_directory_name: DEFAULT
     access_level: none
     vserver: ansibleVServer
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

