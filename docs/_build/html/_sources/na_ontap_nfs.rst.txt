====================================================
na_ontap_nfs - Manage NetApp Ontap NFS service.
====================================================
New in version 2.5.

========
Synopsis
========
Create, delete, start, stop NFS service on SVM.

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
| nfsv3           | Choices:            | status of nfsv3                          |
|                 |                     |                                          |
|                 | * enabled           |                                          |
|                 | * disabled          |                                          |
|                 |                     |                                          |
|                 | Default: None       |                                          |
+-----------------+---------------------+------------------------------------------+
| nfsv4           | Choices:            | status of nfsv4                          |
|                 |                     |                                          |
|                 | * enabled           |                                          |
|                 | * disabled          |                                          |
|                 |                     |                                          |
|                 | Default: None       |                                          |
+-----------------+---------------------+------------------------------------------+
| nfsv41          | Choices:            | status of nfsv41                         |
|                 |                     |                                          |
|                 | * enabled           |                                          |
|                 | * disabled          |                                          |
|                 |                     |                                          |
|                 | Default: None       |                                          |
+-----------------+---------------------+------------------------------------------+
| nfsv4_id_domain | Default: None       | Name of the nfsv4_id_domain to use       |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| service_state   | Choices:            | Whether the specified service should be  |
|                 |                     | running.                                 |
|                 | * started           |                                          |
|                 | * stopped           |                                          |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the NFS service should exist or  |
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
| tcp             | Choices:            | State of tcp to use                      |
|                 |                     |                                          |
|                 | * enabled           |                                          |
|                 | * disabled          |                                          |
|                 |                     |                                          |
|                 | Default: None       |                                          |
+-----------------+---------------------+------------------------------------------+
| udp             | Choices:            | State of udp to use                      |
|                 |                     |                                          |
|                 | * enabled           |                                          |
|                 | * disabled          |                                          |
|                 |                     |                                          |
|                 | Default: None       |                                          |
+-----------------+---------------------+------------------------------------------+
| vserver         |                     | The name of the SVM to use.              |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| vstorage_state  | Default: None       | Status of vstorage state                 |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: change nfs status
   na_ontap_nfs:
     state: present
     service_state: stopped
     vserver: vs_hack
     nfsv3: disabled
     nfsv4: disabled
     nfsv41: enabled
     tcp: disabled
     udp: disabled
     vstorage_state: disabled
     nfsv4_id_domain: example.com
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
