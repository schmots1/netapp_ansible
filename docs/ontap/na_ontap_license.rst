=====================================================================
na_ontap_license - Manage NetApp ONTAP protocol and feature licenses.
=====================================================================
New in version 2.5.

========
Synopsis
========
Add or remove licenses on NetApp ONTAP

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
| https           | Default: false      | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| licenses        |                     | List of licenses to remove. Please       |
|                 |                     | note that trying to remove a non-existant|
|                 |                     | license will throw an error.             |
+-----------------+---------------------+------------------------------------------+
| license_codes   |                     | List of license codes to add             |
+-----------------+---------------------+------------------------------------------+
| fcp             |                     | FCP License                              |
+-----------------+---------------------+------------------------------------------+
| snaplock        |                     | SnapLock License                         |
+-----------------+---------------------+------------------------------------------+
| v_storageattach |                     | Virtual Attached Storage License         |
+-----------------+---------------------+------------------------------------------+
| cifs            |                     | CIFS License                             |
+-----------------+---------------------+------------------------------------------+
| iscsi           |                     | iSCSI License                            |
+-----------------+---------------------+------------------------------------------+
| flexclone       |                     | FlexClone License                        |
+-----------------+---------------------+------------------------------------------+
| cdmi            |                     | CDMI License                             |
+-----------------+---------------------+------------------------------------------+
| snaprestore     |                     | SnapRestore License                      |
+-----------------+---------------------+------------------------------------------+
| snapprotectapps |                     | SnapProtectApp License                   |
+-----------------+---------------------+------------------------------------------+
| base            |                     | Cluster Base License                     |
+-----------------+---------------------+------------------------------------------+
| nfs             |                     | NFS License                              |
+-----------------+---------------------+------------------------------------------+
| snapmirror      |                     | SnapMirror License                       |
+-----------------+---------------------+------------------------------------------+
| snapvault       |                     | SnapVault License                        |
+-----------------+---------------------+------------------------------------------+
| snapmanagersuit |                     | SnapManagerSuit License                  |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| remove_expired  | Choices:            | Remove licenses that have expired in the |
|                 |                     | cluster.                                 |
|                 | * true              |                                          |
|                 | * false             |                                          |
+-----------------+---------------------+------------------------------------------+
| remove_unused   | Choices:            | Remove licenses that have no controller  |
|                 |                     | affiliation in the cluster.              |
|                 | * true              |                                          |
|                 | * false             |                                          |
+-----------------+---------------------+------------------------------------------+
| serial_number   |                     | Serial number of the node associated with|
|                 |                     | the license. This parameter is used      |
|                 |                     | primarily when removing license for a    |
|                 |                     | specific service. If this parameter is   |
|                 |                     | not provided, the cluster serial number  |
|                 |                     | is used by default                       |
+-----------------+---------------------+------------------------------------------+
| username        |                     | This can be a Cluster-scoped or          |
| (required)      |                     | SVM-scoped account, depending on whether |
|                 |                     | a Cluster-level or SVM-level API is      |
|                 |                     | required. For more information, please   |
|                 |                     | read the documentation                   |
|                 |                     | https://goo.gl/BRu78Z.                   |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Add licenses
   na_ontap_license:
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
     serial_number: #################
     license_codes: #################,#################,#################,#################

 - name: Remove licenses
   na_ontap_license:
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
     remove_unused: false
     remove_expired: true
     serial_number: #################
     licenses:
       nfs: remove

