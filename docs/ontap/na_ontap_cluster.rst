=======================================================================
na_ontap_cluster - Create/Join ONTAP cluster.  Apply license to cluster
=======================================================================
New in version 2.5.

========
Synopsis
========
Create, join or apply licenses to ONTAP clusters

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

+--------------------+---------------------+------------------------------------------+
|   Parameter        |   Choices/Defaults  |                 Comments                 |
+--------------------+---------------------+------------------------------------------+
| cluster_ip_address |                     | IP address of cluster to be joined       |
+--------------------+---------------------+------------------------------------------+
| cluster_name       |                     | The name of the cluster to manage        |
+--------------------+---------------------+------------------------------------------+
| hostname           |                     | The hostname or IP address of the ONTAP  |
| (required)         |                     | instance.                                |
+--------------------+---------------------+------------------------------------------+
| https              | Default: false      | Enable and disable https                 |
+--------------------+---------------------+------------------------------------------+
| license_code       |                     | License code to be applied to the cluster|
+--------------------+---------------------+------------------------------------------+
| license_package    |                     | License package name of the license to be|
|                    |                     | removed                                  |
+--------------------+---------------------+------------------------------------------+
| node_serial_number |                     | Serial number of the cluster node        |
+--------------------+---------------------+------------------------------------------+
| password           |                     | Password for the specified user.         |
| (required)         |                     |                                          |
+--------------------+---------------------+------------------------------------------+
| state              | Choices:            | Whether the specified cluster should     |
|                    |                     | exist or not.                            |
|                    | * present (default) |                                          |
|                    | * absent            |                                          |
+--------------------+---------------------+------------------------------------------+
| username           |                     | This can be a Cluster-scoped or          |
| (required)         |                     | SVM-scoped account, depending on whether |
|                    |                     | a Cluster-level or SVM-level API is      |
|                    |                     | required. For more information, please   |
|                    |                     | read the documentation                   |
|                    |                     | https://goo.gl/BRu78Z.                   |
+--------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create cluster
   na_ontap_cluster:
     state: present
     cluster_name: new_cluster
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
 - name: Add license from cluster
   na_ontap_cluster:
     state: present
     cluster_name: FPaaS-A300-01
     license_code: SGHLQDBBVAAAAAAAAAAAAAAAAAAA
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
  - name: Join cluster
   na_ontap_cluster:
     state: present
     cluster_name: FPaaS-A300
     cluster_ip_address: 10.61.184.181
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
