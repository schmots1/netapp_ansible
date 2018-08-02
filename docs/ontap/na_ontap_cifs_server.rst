==============================================================
na_ontap_cifs_server - Manage NetApp cifs server configuration
==============================================================
New in version 2.5.

========
Synopsis
========
Create, modify or destroy CIFS server.

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
| admin_password  |                     | Password for the specified AD admin user |
+-----------------+---------------------+------------------------------------------+
| admin_user_name |                     | Admin user for adding CIFS Server to AD  |
+-----------------+---------------------+------------------------------------------+
| cifs_server_name|                     | Secifies the CIFS server name.           |
+-----------------+---------------------+------------------------------------------+
| hostname        |                     | The hostname or IP address of the ONTAP  |
| (required)      |                     | instance.                                |
+-----------------+---------------------+------------------------------------------+
| https           | Default: false      | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| service_state   |                     | 'CIFS Server Administrative Status.      | 
| (required)      |                     | Values': u'started/stopped               |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the specified CIFS share should  |
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
| vserver         |                     | Name of the SVM to use.                  |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| workgroup       |                     | The NetBIOS name of the domain or        |
|                 |                     | workgroup this CIFS server belongs to    |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create cifs_server
   na_ontap_cifs_server:
     state: present
     vserver: svm1
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: Delete cifs_server
   na_ontap_cifs_server:
     state: absent
     cifs_server_name: data2
     vserver: svm1
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
