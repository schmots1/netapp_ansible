====================================================================
na_elementsw_volume_clone - Create Element Software Volume Clones
====================================================================
New in version 2.6

========
Synopsis
========
Create volume clones on Element software

============
Requirements
============
The below requirements are needed on the host that executes this module.

* An Element software system.  Tested with Element OS 10
* Ansible 2.4 or higher
* solidfire-sdk-python (1.5.0.87). Install using 'pip install solidfire-sdk-python'

==========
Parameters
==========

+----------------------+---------------------+------------------------------------------+
|     Parameter        |   Choices/Defaults  |                 Comments                 |
+----------------------+---------------------+------------------------------------------+
| hostname             |                     | The hostname or IP address of the        |
| (required)           |                     | cluster mvip.                            |
+----------------------+---------------------+------------------------------------------+
| username             |                     | Admin account username.                  |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| password             |                     | Password for the specified username.     |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| src_volume_id        |                     | The ID of the src volume to clone. ID    |
| (required)           |                     | may be a numeric identifier or a volume  |
|                      |                     | name.                                    |
+----------------------+---------------------+------------------------------------------+
| source_snapshot_id   |                     | The ID of the snapshot to clone. ID may  |
|                      |                     | be a numeric identifier or a snapshot    |
|                      |                     | name.                                    |
+----------------------+---------------------+------------------------------------------+
| account_id           |                     | Account ID for the owner of this cloned  |
| (required)           |                     | volume. ID may be a numeric identifier   |
|                      |                     | or an account name.                      |
+----------------------+---------------------+------------------------------------------+
| size                 |                     | The size of the cloned volume in         |
|                      |                     | (size_unit). Required when state=present.|
+----------------------+---------------------+------------------------------------------+
| size_unit            | Choices:            | The unit used to interpret the size      |
|                      |                     | parameter.                               |
|                      | * bytes             |                                          |
|                      | * b                 |                                          |
|                      | * kb                |                                          |
|                      | * mb                |                                          |
|                      | * gb                |                                          |
|                      | * tb                |                                          |
|                      | * pb                |                                          |
|                      | * eb                |                                          |
|                      | * zb                |                                          |
|                      | * yb                |                                          |
|                      |                     |                                          |
|                      | Default: gb         |                                          |
+----------------------+---------------------+------------------------------------------+
| access               | Choices:            | Access allowed for the volume. If the    |
|                      |                     | volume is not paired, the access status  |
|                      | * readOnly          | is locked. If unspecified, the access    |
|                      | * readWrite         | settings of the clone will be the same   |
|                      | * locked            | as the source.                           |
|                      | * replicationTarget |                                          |
+----------------------+---------------------+------------------------------------------+
| attributes           |                     | A YAML dictionary of attributes that you |
|                      |                     | would like to apply on this cloned       |
|                      |                     | volume.                                  |
+----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

    - name: Clone Volume
      na_elementsw_volume_clone:
        hostname: "{{ elementsw_hostname }}"
        username: "{{ elementsw_username }}"
        password: "{{ elementsw_password }}"
        name: CloneAnsibleVol
        src_volume_id: 123
        src_snapshot_id: 41
        account_id: 3
        size: 1
        size_unit: gb
        access: readWrite
        attributes: {"virtual_network_id": 12345}
