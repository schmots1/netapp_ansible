==================================================================
na_ontap_cifs_acl - Manage NetApp ONTAP cifs-share-access-control.
==================================================================
New in version 2.5.

========
Synopsis
========
Create, destroy or modify cifs-share-access-controlls on ONTAP.

============
Requirements
============
The below requirements are needed on the host that executes this module.

* A ONTAP 9 system. The modules were developed with ONTAP 9.3
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
| permission      | Choices:            | {u'read': u'Read,', u'full_control':     |
|                 |                     | u'Full Control,', u'The access rights    |
|                 | * no_access         | that the user or group has on the defined|
|                 | * read              | CIFS share. Possible values': None,      |
|                 | * change            | u'change': u'Change,', u'no_access':     |
|                 | * full_control      | u'No access,'}                           |
+-----------------+---------------------+------------------------------------------+
| share_name      |                     | The name of the cifs-share-access-control|
|                 |                     | to manage                                |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the specified CIFS share acl     |
|                 |                     | should exist or not.                     |
|                 | * present (default) |                                          |
|                 | * absent            |                                          |
+-----------------+---------------------+------------------------------------------+
| user_or_group   |                     | The user or group name for which the     |
|                 |                     | permissions are listed.                  |
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

 - name: Create CIFS share acl
   na_ontap_cifs_acl:
     state: present
     share_name: cifsShareName
     user_or_group: Everyone
     permission: read
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
 - name: Modify CIFS share acl permission
   na_ontap_cifs_acl:
     state: present
     share_name: cifsShareName
     permission: change
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
