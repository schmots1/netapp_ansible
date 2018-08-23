====================================================
na_ontap_fcp - Manage NetApp ONTAP FCP Service.
====================================================
New in version 2.7

========
Synopsis
========
Start, Stop and Enable FCP services.

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
| state           | Choices:            | Whether the fcp service should be        |
|                 |                     | or not.                                  |
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
| status          | Choices:            | Whether the FCP service should be up or  |
|                 |                     | down.                                    |
|                 | * up                |                                          |
|                 | * down              |                                          |
|                 | Default: up         |                                          |
+-----------------+---------------------+------------------------------------------+
| vserver         |                     | The name of the SVM to use.              |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

- name: create FCP
      na_ontap_fcp:
        state: present
        status: down
        hostname: "{{hostname}}"
        username: "{{username}}"
        password: "{{password}}"
        vserver:  "{{vservername}}"
