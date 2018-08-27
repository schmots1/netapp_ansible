====================================================
na_ontap_ntp - Manage NetApp ONTAP NTP server.
====================================================
New in version 2.5.

========
Synopsis
========
Create, delete or modify NTP server in ONTAP

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

+-----------------+---------------------+------------------------------------------+
|   Parameter     |   Choices/Defaults  |                 Comments                 |
+-----------------+---------------------+------------------------------------------+
| hostname        |                     | The hostname or IP address of the ONTAP  |
| (required)      |                     | instance.                                |
+-----------------+---------------------+------------------------------------------+
| https           | Default: false      | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| validate_certs  | Default: true       | Set to false in order to use self-signed |
|                 |                     | certificates with https.  *Warning: this |
|                 |                     | does open up the small possiblity of a   |
|                 |                     | man-in-the-middle attack.                |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| server_name     |                     | The name of the NTP server to manage.    |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the specified NTP servershould   |
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
| version         | Choices:            | Version for NTP server                   |
|                 |                     |                                          |
|                 | * auto              |                                          |
|                 | * 3                 |                                          |
|                 | * 4                 |                                          |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create NTP server
   na_ontap_ntp:
     state: present
     version: auto
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
 
 - name: Delete NTP server
   na_ontap_ntp:
     state: absent
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
