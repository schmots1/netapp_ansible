====================================================
na_ontap_iscsi - Manage NetApp Ontap iscsi service.
====================================================
New in version 2.5.

========
Synopsis
========
Create, delete, start, stop iscsi service on SVM.

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
| hostname        |                     | The hostname or IP address of the ONTAP  |
| (required)      |                     | instance.                                |
+-----------------+---------------------+------------------------------------------+
| https           | Default: false      | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| service_state   | Choices:            | Whether the specified service should be  |
|                 |                     | running.                                 |
|                 | * started           |                                          |
|                 | * stopped           |                                          |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the iscsi service should exist or|
|                 |                     | not.                                     |
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
| vserver         |                     | The name of the SVM to use.              |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create iscsi service
   na_ontap_iscsi:
     state: started
     vserver: ansibleVServer
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: Stop Iscsi service
   na_ontap_iscsi:
     state: stopped
     vserver: ansibleVServer
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: Delete Iscsi service
   na_ontap_iscsi:
     state: absent
     vserver: ansibleVServer
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
