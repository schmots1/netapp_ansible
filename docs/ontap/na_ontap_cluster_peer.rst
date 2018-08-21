=======================================================================
na_ontap_cluster_peer - Manage NetApp ONTAP Cluster Peer Relationships.
=======================================================================
New in version 2.7

========
Synopsis
========
Create/Delete cluster peer relations on ONTAP

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

+-------------------------+---------------------+------------------------------------------+
|        Parameter        |   Choices/Defaults  |                 Comments                 |
+-------------------------+---------------------+------------------------------------------+
| state                   | Choices:            | Whether the specified cluster peer       |
|                         |                     | should exist or not.                     |
|                         | * present (default) |                                          |
|                         | * absent            |                                          |
+-------------------------+---------------------+------------------------------------------+
| hostname                |                     | The hostname or IP address of the ONTAP  |
| (required)              |                     | instance.                                |
+-------------------------+---------------------+------------------------------------------+
| username                |                     | This can be a Cluster-scoped or          |
| (required)              |                     | SVM-scoped account, depending on whether |
|                         |                     | a Cluster-level or SVM-level API is      |
|                         |                     | required. For more information, please   |
|                         |                     | read the documentation                   |
|                         |                     | https://goo.gl/BRu78Z.                   |
+-------------------------+---------------------+------------------------------------------+
| password                |                     | Password for the specified user.         |
| (required)              |                     |                                          |
+-------------------------+---------------------+------------------------------------------+
| https                   | Default: false      | Enable and disable https                 |
+-------------------------+---------------------+------------------------------------------+
| validate_certs          | Default: true       | Set to false in order to use self-signed |
|                         |                     | certificates with https.  *Warning: this |
|                         |                     | does open up the small possiblity of a   |
|                         |                     | man-in-the-middle attack.                |
+-------------------------+---------------------+------------------------------------------+
| dest_cluster_name       |                     | The name of the destination cluster name |
|                         |                     | in the peer relation to be deleted.      |
+-------------------------+---------------------+------------------------------------------+
| dest_hostname           |                     | Destination cluster IP or hostname which |
|                         |                     | needs to be peered.                      |
+-------------------------+---------------------+------------------------------------------+
| dest_intercluster_lif   |                     | Intercluster address of the destination  |
|                         |                     | cluster.  Used as peer-address in source |
|                         |                     | cluster.                                 |
+-------------------------+---------------------+------------------------------------------+
| dest_password           |                     | Destination password.  Optional if this  |
|                         |                     | is same as source password.              |
+-------------------------+---------------------+------------------------------------------+
| dest_username           |                     | Destination username.  Optional if this  |
|                         |                     | is same as source username.              |
+-------------------------+---------------------+------------------------------------------+
| passphrase              |                     | The arbitrary passphrase that matches    |
|                         |                     | the one given to the peer cluster.       |
+-------------------------+---------------------+------------------------------------------+
| source_cluster_name     |                     | The name of the source cluster name in   |
|                         |                     | the peer relation to be deleted.         |
+-------------------------+---------------------+------------------------------------------+
| source_intercluster_lif |                     | Intercluster address of the source       |
|                         |                     | cluster. Used as peer-address in         |
|                         |                     | destination cluster.                     |
+-------------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

    - name: Create cluster peer
      na_ontap_cluster_peer:
        state: present
        source_intercluster_lif: 1.2.3.4
        dest_intercluster_lif: 5.6.7.8
        passphrase: XXXX
        hostname: "{{ netapp_hostname }}"
        username: "{{ netapp_username }}"
        password: "{{ netapp_password }}"
        dest_hostname: "{{ netapp_hostname }}"

    - name: Delete cluster peer
      na_ontap_cluster_peer:
        state: absent
        source_cluster_name: test-source-cluster
        dest_cluster_name: test-dest-cluster
        hostname: "{{ netapp_hostname }}"
        username: "{{ netapp_username }}"
        password: "{{ netapp_password }}"
        dest_hostname: "{{ netapp_hostname }}"
