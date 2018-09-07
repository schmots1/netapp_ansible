====================================================
na_ontap_snapmirr - Manage NetApp ONTAP SnapMirrors.
====================================================
New in version 2.7

========
Synopsis
========
Create/Delete/Initialize/Modify SnapMirror volume/vserver relationships.

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

+---------------------+------------------------------+------------------------------------------+
|      Parameter      |       Choices/Defaults       |                 Comments                 |
+---------------------+------------------------------+------------------------------------------+
| state               | Choices:                     | Whether the specified relationship       |
|                     |                              | should exist or not.                     |
|                     | * present (default)          |                                          |
|                     | * absent                     |                                          |
+---------------------+------------------------------+------------------------------------------+
| hostname            |                              | The hostname or IP address of the ONTAP  |
| (required)          |                              | instance.                                |
+---------------------+------------------------------+------------------------------------------+
| username            |                              | This can be a Cluster-scoped or          |
| (required)          |                              | SVM-scoped account, depending on whether |
|                     |                              | a Cluster-level or SVM-level API is      |
|                     |                              | required. For more information, please   |
|                     |                              | read the documentation                   |
|                     |                              | https://goo.gl/BRu78Z.                   |
+---------------------+------------------------------+------------------------------------------+
| password            |                              | Password for the specified user.         |
| (required)          |                              |                                          |
+---------------------+------------------------------+------------------------------------------+
| https               | Default: false               | Enable and disable https                 |
+---------------------+------------------------------+------------------------------------------+
| validate_certs      | Default: true                | Set to false in order to use self-signed |
|                     |                              | certificates with https.  *Warning: this |
|                     |                              | does open up the small possiblity of a   |
|                     |                              | man-in-the-middle attack.                |
+---------------------+------------------------------+------------------------------------------+
| destination_path    |                              | Specifies the destination endpoint of    |
|                     |                              | the SnapMirror relationship.             |
+---------------------+------------------------------+------------------------------------------+
| destination_volume  |                              | Specifies the name of the destination    |
|                     |                              | volume for the SnapMirror.               |
+---------------------+------------------------------+------------------------------------------+
| destination_vserver |                              | Name of the destination vserver for the  |
|                     |                              | SnapMirror.                              |
+---------------------+------------------------------+------------------------------------------+
| relationship_type   | Choices:                     | Specify the type of SnapMirror           |
|                     |                              | relationship.                            |
|                     | * data_protection            |                                          |
|                     | * load_sharing               |                                          |
|                     | * vault                      |                                          |
|                     | * restore                    |                                          |
|                     | * transition_data_protection |                                          |
|                     | * extended_data_protection   |                                          |
+---------------------+------------------------------+------------------------------------------+
| schedule            |                              | Specify the name of the current          |
|                     |                              | schedule, which is used to update the    |
|                     |                              | SnapMirror relationship. Optional for    |
|                     |                              | create, modifiable.                      |
+---------------------+------------------------------+------------------------------------------+
| source_hostname     |                              | Source hostname or IP address. Required  |
|                     |                              | for SnapMirror delete                    |
+---------------------+------------------------------+------------------------------------------+
| source_password     |                              | Source password. Optional if this is     |
|                     |                              | same as destination password.            |
+---------------------+------------------------------+------------------------------------------+
| source_path         |                              | Specifies the source endpoint of the     |
|                     |                              | SnapMirror relationship.                 |
+---------------------+------------------------------+------------------------------------------+
| source_username     |                              | Source username. Optional if this is     |
|                     |                              | same as destination username.            |
+---------------------+------------------------------+------------------------------------------+
| source_volume       |                              | Specifies the name of the source volume  |
|                     |                              | for the SnapMirror.                      |
+---------------------+------------------------------+------------------------------------------+
| source_vserver      |                              | Name of the source vserver for the       |
|                     |                              | SnapMirror.                              |
+---------------------+------------------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples:

- name: Create SnapMirror
      na_ontap_snapmirror:
        state: present

        source_volume: test_src

        destination_volume: test_dest

        source_vserver: ansible_src

        destination_vserver: ansible_dest

        hostname: "{{ netapp_hostname }}"

        username: "{{ netapp_username }}"

        password: "{{ netapp_password }}"

    - name: Delete SnapMirror
      na_ontap_snapmirror:
        state: absent
        destination_path: <path>
        hostname: "{{ netapp_hostname }}"
        username: "{{ netapp_username }}"
        password: "{{ netapp_password }}"

    - name: Set schedule to NULL
      na_ontap_snapmirror:
        state: present
        destination_path: <path>
        schedule: ""
        hostname: "{{ netapp_hostname }}"
        username: "{{ netapp_username }}"
        password: "{{ netapp_password }}"

    - name: Release SnapMirror
      na_ontap_snapmirror:
        state: release
        destination_path: <path>
        hostname: "{{ netapp_hostname }}"
        username: "{{ netapp_username }}"
        password: "{{ netapp_password }}"
