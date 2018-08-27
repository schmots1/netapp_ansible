===============================================================
na_ontap_software_update- Manage NetApp ONTAP Software Updates.
===============================================================
New in version 2.7

========
Synopsis
========
Update ONTAP software

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

+---------------------------+---------------------+------------------------------------------+
|         Parameter         |   Choices/Defaults  |                 Comments                 |
+---------------------------+---------------------+------------------------------------------+
| state                     | Choices:            | Whether the specified ONTAP package      |
|                           |                     | should exist or not.                     |
|                           | * present (default) |                                          |
|                           | * absent            |                                          |
+---------------------------+---------------------+------------------------------------------+
| hostname                  |                     | The hostname or IP address of the ONTAP  |
| (required)                |                     | instance.                                |
+---------------------------+---------------------+------------------------------------------+
| username                  |                     | This can be a Cluster-scoped or          |
| (required)                |                     | SVM-scoped account, depending on whether |
|                           |                     | a Cluster-level or SVM-level API is      |
|                           |                     | required. For more information, please   |
|                           |                     | read the documentation                   |
|                           |                     | https://goo.gl/BRu78Z.                   |
+---------------------------+---------------------+------------------------------------------+
| password                  |                     | Password for the specified user.         |
| (required)                |                     |                                          |
+---------------------------+---------------------+------------------------------------------+
| https                     | Default: false      | Enable and disable https                 |
+---------------------------+---------------------+------------------------------------------+
| validate_certs            | Default: true       | Set to false in order to use self-signed |
|                           |                     | certificates with https.  *Warning: this |
|                           |                     | does open up the small possiblity of a   |
|                           |                     | man-in-the-middle attack.                |
+---------------------------+---------------------+------------------------------------------+
| ignore_validation_warning |                     | Allows the update to continue if         |
|                           |                     | warnings are encountered during the      |
|                           |                     | validation phase.                        |
+---------------------------+---------------------+------------------------------------------+
| node                      |                     | List of nodes to be updated, the nodes   |
|                           |                     | have to be a part of a HA Pair.          |
+---------------------------+---------------------+------------------------------------------+
| package_url               |                     | Specifies the package URL.               |
| (required)                |                     |                                          |
+---------------------------+---------------------+------------------------------------------+
| package_version           |                     | Specifies the package version.           |
| (required)                |                     |                                          |
+---------------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

- name: ONTAP software update
      na_ontap_software_update:
        state: present
        node: laurentn-vsim1
        package_url: "{{ url }}"
        package_version: "{{ version_name }}"
        ignore_validation_warning: True
        hostname: "{{ netapp_hostname }}"
        username: "{{ netapp_username }}"
        password: "{{ netapp_password }}"
