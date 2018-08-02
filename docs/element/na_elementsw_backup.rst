=================================================================
na_elementsw_backup - Element Software Backup Manager
=================================================================
New in version 2.6

========
Synopsis
========
Create Element Software Backups

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
| src_hostname         |                     | The hostname or IP address of the backup |
| (required)           |                     | source cluster mvip.                     |
+----------------------+---------------------+------------------------------------------+
| src_username         |                     | Admin account username of backup source  |
| (required)           |                     | cluster.                                 |
+----------------------+---------------------+------------------------------------------+
| src_password         |                     | Password for the specified username of   |
| (required)           |                     | backup source cluster.                   |
+----------------------+---------------------+------------------------------------------+
| src_volume_id        |                     | ID of the backup source volume.          |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| dest_hostname        |                     | The hostname or IP address of the        |
| (required)           |                     | destination cluster mvip.                |
+----------------------+---------------------+------------------------------------------+
| dest_username        |                     | Admin account username of backup         |
| (required)           |                     | destination cluster.                     |
+----------------------+---------------------+------------------------------------------+
| dest_password        |                     | Password for the specified username of   |
| (required)           |                     | backup destination cluster.              |
+----------------------+---------------------+------------------------------------------+
| dest_volume_id       |                     | ID of the backup destination volume.     |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| format               | Choices:            | Backup format to use.                    |
|                      |                     |                                          |
|                      | * native (default)  |                                          |
|                      | * uncompressed      |                                          |
+----------------------+---------------------+------------------------------------------+
| script               |                     | The backup script to be executed.        |
+----------------------+---------------------+------------------------------------------+
| script_parameters    |                     | The backup script parameters.            | 
+----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

na_elementsw_backup:
  src_hostname: "{{ source_cluster_hostname }}"
  src_username: "{{ source_cluster_username }}"
  src_password: "{{ source_cluster_password }}"
  src_volume_id: 1
  dest_hostname: "{{ destination_cluster_hostname }}"
  dest_username: "{{ destination_cluster_username }}"
  dest_password: "{{ destination_cluster_password }}"
  dest_volume_id: 3
  format: native
