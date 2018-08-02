=================================================================
na_elementsw_cluster - Manage Element Software Cluster Creation
=================================================================
New in version 2.6

========
Synopsis
========
Initialize Element Software node ownership to form a cluster.

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

+------------------------+---------------------+------------------------------------------+
|     Parameter          |   Choices/Defaults  |                 Comments                 |
+------------------------+---------------------+------------------------------------------+
| hostname               |                     | The hostname or IP address of the        |
| (required)             |                     | cluster mvip.                            |
+------------------------+---------------------+------------------------------------------+
| username               |                     | Admin account username.                  |
| (required)             |                     |                                          |
+------------------------+---------------------+------------------------------------------+
| password               |                     | Password for the specified username.     |
| (required)             |                     |                                          |
+------------------------+---------------------+------------------------------------------+
| management_virtual_ip  |                     | Floating (virtual) IP address for the    |
| (required)             |                     | cluster on the management network.       |
+------------------------+---------------------+------------------------------------------+
| storage_virtual_ip     |                     | Floating (virtual) IP address for the    |
| (required)             |                     | cluster on the storage (iSCSI) network.  |
+------------------------+---------------------+------------------------------------------+
| replica_count          | Default: 2          | Number of replicas of each piece of data |
|                        |                     | to store in the cluster.                 |
+------------------------+---------------------+------------------------------------------+
| cluster_admin_username |                     | Username for the cluster admin.          |
|                        |                     | If not provided, default to login        |
|                        |                     | username.                                |
+------------------------+---------------------+------------------------------------------+
| cluster_admin_password |                     | Initial password for the cluster admin   |
|                        |                     | account. If not provided, default to     |
|                        |                     | login password.                          |
+------------------------+---------------------+------------------------------------------+
| accept_eula            |                     | Required to indicate your acceptance of  |
|                        |                     | the End User License Agreement when      |
|                        |                     | creating this cluster. To accept the     |
|                        |                     | EULA, set this parameter to true.        |
+------------------------+---------------------+------------------------------------------+
| nodes                  |                     | Storage IP (SIP) addresses of the        |
|                        |                     | initial set of nodes making up the       |
|                        |                     | cluster. Nodes IP must be in the list.   |
+------------------------+---------------------+------------------------------------------+
| attributes             |                     | List of name-value pairs in JSON object  |
|                        |                     | format.                                  |
+------------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

  - name: Initialize new cluster
    tags:
    - elementsw_cluster
    na_elementsw_cluster:
      hostname: "{{ elementsw_hostname }}"
      username: "{{ elementsw_username }}"
      password: "{{ elementsw_password }}"
      management_virtual_ip: 10.226.108.32
      storage_virtual_ip: 10.226.109.68
      replica_count: 2
      cluster_admin_username: admin
      cluster_admin_password: netapp123
      accept_eula: true
      nodes:
      - 10.226.109.72
      - 10.226.109.74
