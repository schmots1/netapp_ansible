==============================================
na_ontap_cifs - Manage NetApp ONTAP cifs-share
==============================================
New in version 2.5.

========
Synopsis
========
Create, destroy or modify(path) cifs-share on ONTAP.

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
| path            | Choices:            | The file system path that is shared      |
|                 |                     | through this CIFS share.  The path is the|
|                 |                     | full, user visible path relative to the  |
|                 |                     | SVM root, and it might be crossing       |
|                 |                     | junction mount points.  The path is in   |
|                 |                     | UTF8 and uses forward slash as directory |
|                 |                     | separator                                |
+-----------------+---------------------+------------------------------------------+
| share_name      |                     | The name of the cifs-share-access-control|
|                 |                     | to manage                                |
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
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create CIFS share
   na_ontap_cifs:
     state: present
     share_name: cifsShareName
     path: /
     vserver: vserverName
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
 - name: Delete CIFS share
   na_ontap_cifs:
     state: absent
     share_name: cifsShareName
     vserver: vserverName
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
 - name: Modify path CIFS share
   na_ontap_cifs:
     state: present
     share_name: pb_test
     vserver: vserverName
     path: /
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

