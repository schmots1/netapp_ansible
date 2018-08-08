=================================================================
na_elementsw_snapshot - Manage Element Software Snapshots
=================================================================
New in version 2.6

========
Synopsis
========
Create, modify or delete snapshot on Element software cluster.

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

+---------------------------+---------------------+------------------------------------------+
|        Parameter          |   Choices/Defaults  |                 Comments                 |
+---------------------------+---------------------+------------------------------------------+
| state                     | Choices:            | Whether the specified snapshot should    |
|                           |                     | exist or not.                            |
|                           | * present           |                                          |
|                           | * absent            |                                          |
+---------------------------+---------------------+------------------------------------------+
| hostname                  |                     | The hostname or IP address of the        |
| (required)                |                     | cluster mvip.                            |
+---------------------------+---------------------+------------------------------------------+
| username                  |                     | Admin account username.                  |
| (required)                |                     |                                          |
+---------------------------+---------------------+------------------------------------------+
| password                  |                     | Password for the specified username.     |
| (required)                |                     |                                          |
+---------------------------+---------------------+------------------------------------------+
| src_volume_id             |                     | ID or name of active volume.             |
| (required)                |                     |                                          |
+---------------------------+---------------------+------------------------------------------+
| account_id                |                     | Account ID or Name of Parent/Source      |
| (required)                |                     | Volume.                                  | 
+---------------------------+---------------------+------------------------------------------+
| retention                 |                     | Retention period for the snapshot.       |
|                           |                     | Format is 'HH:mm:ss'.                    |
+---------------------------+---------------------+------------------------------------------+
| src_snapshot_id           |                     | ID or Name of an existing snapshot.      |
|                           |                     | Required when state=present, to modify   |
|                           |                     | snapshot properties. Required when       |
|                           |                     | state=present, to create snapshot from   |
|                           |                     | another snapshot in the volume. Required |
|                           |                     | when state=absent, to delete snapshot.   |
+---------------------------+---------------------+------------------------------------------+
| enable_remote_replication |                     | Flag, whether to replicate the snapshot  |
|                           |                     | created to a remote replication cluster. |
|                           |                     | To enable specify 'true' value.          |
+---------------------------+---------------------+------------------------------------------+
| snap_mirror_label         |                     | Label used by SnapMirror software to     |
|                           |                     | specify snapshot retention policy on     |
|                           |                     | SnapMirror endpoint.                     |
+---------------------------+---------------------+------------------------------------------+
| expiration_time           |                     | The date and time (format ISO 8601 date  |
|                           |                     | string) at which this snapshot will      |
|                           |                     | expire.                                  |
+---------------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

   - name: Create snapshot
     tags:
     - elementsw_create_snapshot
     na_elementsw_snapshot:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: present
       src_volume_id: 118
       account_id: sagarsh
       name: newsnapshot-1

   - name: Modify Snapshot
     tags:
     - elementsw_modify_snapshot
     na_elementsw_snapshot:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: present
       src_volume_id: sagarshansivolume
       src_snapshot_id: test1
       account_id: sagarsh
       expiration_time: '2018-06-16T12:24:56Z'
       enable_remote_replication: false

   - name: Delete Snapshot
     tags:
     - elementsw_delete_snapshot
     na_elementsw_snapshot:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: absent
       src_snapshot_id: deltest1
       account_id: sagarsh
       src_volume_id: sagarshansivolume
