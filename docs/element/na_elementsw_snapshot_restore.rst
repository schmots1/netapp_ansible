=================================================================
na_elementsw_snapshot_restore - Element Software Snapshot Restore
=================================================================
New in version 2.6

========
Synopsis
========
Element OS Software restore snapshot to active volume.

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
| src_volume_id        |                     | ID or Name of source active volume.      |
| (required)           |                     |                                          | 
+----------------------+---------------------+------------------------------------------+
| src_snapshot_id      |                     | ID or Name of an existing snapshot.      |
| (required)           |                     |                                          | 
+----------------------+---------------------+------------------------------------------+
| dest_volume_name     |                     | New Name of destination for restoring    |
| (required)           |                     | the snapshot.                            | 
+----------------------+---------------------+------------------------------------------+
| account_id           |                     | Account ID or Name of Parent/Source      |
| (required)           |                     | Volume.                                  | 
+----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

   - name: Restore snapshot to volume
     tags:
     - elementsw_create_snapshot_restore
     na_elementsw_snapshot_restore:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       account_id: ansible-1
       src_snapshot_id: snapshot_20171021
       src_volume_id: volume-playarea
       dest_volume_name: dest-volume-area
