====================================================
na_ontap_lun_map - Manage NetApp ONTAP LUN maps
====================================================
New in version 2.5.

========
Synopsis
========
Map and unmap luns on NetApp ONTAP

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

+------------------------+---------------------+------------------------------------------+
|   Parameter            |   Choices/Defaults  |                 Comments                 |
+------------------------+---------------------+------------------------------------------+
| hostname               |                     | The hostname or IP address of the ONTAP  |
| (required)             |                     | instance.                                |
+------------------------+---------------------+------------------------------------------+
| https                  | Default: false      | Enable and disable https                 |
+------------------------+---------------------+------------------------------------------+
| initiator_group_name   |                     | Initiator group to map to the given LUN  |
+------------------------+---------------------+------------------------------------------+
| lun_id                 |                     | LUN ID assigned for hte map.             |
+------------------------+---------------------+------------------------------------------+
| password               |                     | Password for the specified user.         |
| (required)             |                     |                                          |
+------------------------+---------------------+------------------------------------------+
| path                   |                     | Path of the LUN.                         |
|                        |                     | Required when state=present.             |
+------------------------+---------------------+------------------------------------------+
| state                  | Choices:            | Whether the specified aggregate should   |
|                        |                     | exist or not.                            |
|                        | * present (default) |                                          |
|                        | * absent            |                                          |
+------------------------+---------------------+------------------------------------------+
| username               |                     | This can be a Cluster-scoped or          |
| (required)             |                     | SVM-scoped account, depending on whether |
|                        |                     | a Cluster-level or SVM-level API is      |
|                        |                     | required. For more information, please   |
|                        |                     | read the documentation                   |
|                        |                     | https://goo.gl/BRu78Z.                   |
+------------------------+---------------------+------------------------------------------+
| vserver                |                     | The name of the SVM to use               |
| (required)             |                     |                                          |
+------------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create lun mapping
   na_ontap_lun_map:
     state: present
     initiator_group_name: ansibleIgroup3234
     path: /vol/iscsi_path/iscsi_lun
     vserver: ci_dev
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: Unmap Lun
   na_ontap_lun_map:
     state: absent
     initiator_group_name: ansibleIgroup3234
     path: /vol/iscsi_path/iscsi_lun
     vserver: ci_dev
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
