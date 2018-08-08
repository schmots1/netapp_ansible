=====================================================
na_elementsw_volume - Manage Element Software Volumes
=====================================================
New in version 2.6

========
Synopsis
========
Create, destroy, or update volumes on Element software

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
| state                | Choices:            | Whether the specified volume should      |
|                      |                     | exist or not.                            |
|                      | * present           |                                          |
|                      | * absent            |                                          |
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
| name                 |                     | The name of the volume to manage. It     |
| (required)           |                     | accepts volume_name or volume_id.        |
+----------------------+---------------------+------------------------------------------+
| account_id           |                     | Account ID for the owner of this volume. |
| (required)           |                     | It accepts Account id or Account name.   |
+----------------------+---------------------+------------------------------------------+
| enable512e           |                     | Should the volume provide 512-byte       |
|                      |                     | sector emulation? Required when          |
|                      |                     | state=present.                           |
+----------------------+---------------------+------------------------------------------+
| qos                  |                     | Initial quality of service settings for  |
|                      |                     | this volume. Configure as dict in        |
|                      |                     | playbooks.                               |
+----------------------+---------------------+------------------------------------------+
| attributes           |                     | A YAML dictionary of attributes that you |
|                      |                     | would like to apply on this volume.      |
+----------------------+---------------------+------------------------------------------+
| size                 |                     | The size of the volume in (size_unit).   |
|                      |                     | Required when state = present.           |
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

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

- name: Create Volume
     na_elementsw_volume:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: present
       name: AnsibleVol
       qos: {minIOPS: 1000, maxIOPS: 20000, burstIOPS: 50000}
       account_id: 3
       enable512e: False
       size: 1
       size_unit: gb

   - name: Update Volume
     na_elementsw_volume:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: present
       name: AnsibleVol
       account_id: 3
       access: readWrite

   - name: Delete Volume
     na_elementsw_volume:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: absent
       name: AnsibleVol
       account_id: 2
