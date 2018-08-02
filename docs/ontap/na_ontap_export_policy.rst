=============================================================
na_ontap_export_policy - Manage NetApp ONTAP export policies.
=============================================================
New in version 2.5.

========
Synopsis
========
Create, destroy or rename export policies on ONTAP

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
| https           | Default: no         | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| name            |                     | The name of the export-policy to manage. |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| new_name        |                     | The name of the export-policy to be      |
|                 |                     | renamed                                  |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the specified aggregate should   |
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

 - name: Create Export Policy
   na_ontap_export_policy:
     state: present
     name: ansiblePolicyName
     vserver=vs_hack
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
 - name: Rename Export Policy
   na_ontap_export_policy:
     action: present
     name: ansiblePolicyName
     vserver=vs_hack
     new_name: newPolicyName
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
 - name: Delete Export Policy
   na_ontap_export_policy:
     state: absent
     name: ansiblePolicyName
     vserver=vs_hack
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
