====================================================
na_ontap_disks - Manage NetApp ONTAP Disk Assign
====================================================
New in version 2.7

========
Synopsis
========
Assign all disks to nodes.

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
| state           | Choices:            | Place holder for disk unassign.          |
|                 |                     |                                          |
|                 | * present (default) |                                          |
|                 | * absent            |                                          |
+-----------------+---------------------+------------------------------------------+
| hostname        |                     | The hostname or IP address of the ONTAP  |
| (required)      |                     | instance.                                |
+-----------------+---------------------+------------------------------------------+
| username        |                     | This can be a Cluster-scoped or          |
| (required)      |                     | SVM-scoped account, depending on whether |
|                 |                     | a Cluster-level or SVM-level API is      |
|                 |                     | required. For more information, please   |
|                 |                     | read the documentation                   |
|                 |                     | https://goo.gl/BRu78Z.                   |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| https           | Default: false      | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| validate_certs  | Default: true       | Set to false in order to use self-signed |
|                 |                     | certificates with https.  *Warning: this |
|                 |                     | does open up the small possiblity of a   |
|                 |                     | man-in-the-middle attack.                |
+-----------------+---------------------+------------------------------------------+
| node            |                     | It specifies the node to which           |
|                 |                     | autoassignment or assignment of all      |
|                 |                     | unowned disks must be done.              |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

- name: Assign unowned disks
  na_ontap_disks:
    state: present
    node: cluster-01
    hostname: "{{ hostname }} "
    username: "{{ admin username }}"
    password: "{{ admin password }}"
