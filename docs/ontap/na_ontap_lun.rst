====================================================
na_ontap_lun - Manage NetApp ONTAP LUNs
====================================================
New in version 2.5.

========
Synopsis
========
Create, destroy or resize luns on NetApp ONTAP

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
| flexvol_name           |                     | The name of the FlexVol the LUN should   |
| (required)             |                     | exist on.                                |
+------------------------+---------------------+------------------------------------------+
| force_remove           | Default: false      | If "true", override checks that prevent a|
|                        |                     | LUN from being destroyed if it is online |
|                        |                     | and mapped. If "false", destroying an    |
|                        |                     | online and mapped LUN will fail.         |
+------------------------+---------------------+------------------------------------------+
| force_remove_fenced    | Default: false      | If "true", override checks that prevent a|
|                        |                     | LUN from being destroyed while it is     |
|                        |                     | fenced. If "false", attempting to destroy|
|                        |                     | a fenced LUN will fail.                  |
+------------------------+---------------------+------------------------------------------+
| force_resize           | Default: false      | Forcibly reduce the size. This is        |
|                        |                     | required for reducing the size of the LUN|
|                        |                     | to avoid accidentally reducing the LUN   |
|                        |                     | size.                                    |
+------------------------+---------------------+------------------------------------------+
| hostname               |                     | The hostname or IP address of the ONTAP  |
| (required)             |                     | instance.                                |
+------------------------+---------------------+------------------------------------------+
| https                  | Default: false      | Enable and disable https                 |
+------------------------+---------------------+------------------------------------------+
| name                   |                     | The name of the LUN to manage.           |
| (required)             |                     |                                          |
+------------------------+---------------------+------------------------------------------+
| ostype                 | Default: image      | The OS type for the LUN.                 |
+------------------------+---------------------+------------------------------------------+
| password               |                     | Password for the specified user.         |
| (required)             |                     |                                          |
+------------------------+---------------------+------------------------------------------+
| size                   |                     | The size of the LUN in size_unit.        |
|                        |                     | Required when state=present.             |
+------------------------+---------------------+------------------------------------------+
| size_unit              | Choices:            | The unit used to interpret the size      |
|                        |                     | parameter.                               |
|                        | * bytes             |                                          |
|                        | * b                 |                                          |
|                        | * kb                |                                          |
|                        | * mb                |                                          |
|                        | * gb (default)      |                                          |
|                        | * tb                |                                          |
|                        | * pb                |                                          |
|                        | * eb                |                                          |
|                        | * zb                |                                          |
|                        | * yb                |                                          |
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

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create LUN
   na_ontap_lun:
     state: present
     name: ansibleLUN
     flexvol_name: ansibleVolume
     vserver: ansibleVServer
     size: 5
     size_unit: mb
     ostype: linux
     space_reserve: True
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: Resize Lun
   na_ontap_lun:
     state: present
     name: ansibleLUN
     force_resize: True
     flexvol_name: ansibleVolume
     vserver: ansibleVServer
     size: 5
     size_unit: gb
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}" 
