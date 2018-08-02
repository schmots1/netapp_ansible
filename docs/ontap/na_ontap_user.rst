====================================================
na_ontap_user - Manage NetApp ONTAP Users.
====================================================
New in version 2.5.

========
Synopsis
========
Create and destroy users.

============
Requirements
============
The below requirements are needed on the host that executes this module.

* An ONTAP 9 system. The modules were developed with  ONTAP 9.3
* Ansible 2.4 or higher
* netapp-lib (2017.10.30). Install using 'pip install netapp-lib'

==========
Parameters
==========

+-----------------------+---------------------+------------------------------------------+
|   Parameter           |   Choices/Defaults  |                 Comments                 |
+-----------------------+---------------------+------------------------------------------+
| application           | Choices:            | Applications to grant access to.         | 
| (required)            |                     |                                          |
|                       | * console           |                                          |
|                       | * http              |                                          |
|                       | * ontapi            |                                          |
|                       | * rsh               |                                          |
|                       | * snmp              |                                          |
|                       | * sp                |                                          |
|                       | * ssh               |                                          |
|                       | * telnet            |                                          |
+-----------------------+---------------------+------------------------------------------+
| authentication_method | Choices:            | Authentication method for the application|
| (required)            |                     |                                          |
|                       | * community         |                                          |
|                       | * password          |                                          |
|                       | * publickey         |                                          |
|                       | * domain            |                                          |
|                       | * nsswitch          |                                          |
|                       | * usm               |                                          |
+-----------------------+---------------------+------------------------------------------+
| hostname              |                     | The hostname or IP address of the ONTAP  |
| (required)            |                     | instance.                                |
+-----------------------+---------------------+------------------------------------------+
| https                 | Default: false      | Enable and disable https                 |
+-----------------------+---------------------+------------------------------------------+
| lock_user             |                     | To lock/unlock user.                     |
+-----------------------+---------------------+------------------------------------------+
| role_name             |                     | The name of the role. Required when      |
|                       |                     | state=present                            |
+-----------------------+---------------------+------------------------------------------+
| password              |                     | Password for the specified user.         |
| (required)            |                     |                                          |
+-----------------------+---------------------+------------------------------------------+
| set_password          |  Default: None      | Password for the user account            | 
+-----------------------+---------------------+------------------------------------------+
| state                 | Choices:            | Whether the specified user should        |
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
| vserver               |                     | The name of the SVM to use               |
+-----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create User
   na_ontap_user:
     state: present
     name: SampleUser
     application: ssh
     authentication_method: password
     set_password: apn1242183u1298u41
     lock_user: True
     role_name: vsadmin
     vserver: ansibleVServer
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
