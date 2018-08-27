=======================================================================
na_ontap_vserver_peer - Manage NetApp ONTAP SVM Peer Relationships.
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
| state                   | Choices:            | Whether the specified SVM  peer          |
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
| dest_hostname           |                     | Destination cluster IP or hostname which |
|                         |                     | needs to be peered.                      |
+-------------------------+---------------------+------------------------------------------+
| dest_password           |                     | Destination password.  Optional if this  |
|                         |                     | is same as source password.              |
+-------------------------+---------------------+------------------------------------------+
| dest_username           |                     | Destination username.  Optional if this  |
|                         |                     | is same as source username.              |
+-------------------------+---------------------+------------------------------------------+
| peer_cluster            |                     | Specifies name of the peer Cluster. If   |
|                         |                     | peer Cluster is not given, it considers  |
|                         |                     | local Cluster.                           |
+-------------------------+---------------------+------------------------------------------+
| peer_vserver            |                     | Specifies name of the peer Vserver in    |
|                         |                     | the relationship.                        |
+-------------------------+---------------------+------------------------------------------+
| vserver                 |                     | Specifies name of the source Vserver in  |
|                         |                     | the relationship.                        |
+-------------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

- name: Source vserver peer create
      na_ontap_vserver_peer:
        state: present
        peer_vserver: ansible2
        peer_cluster: ansibleCluster
        vserver: ansible
        applications: snapmirror
        hostname: "{{ netapp_hostname }}"
        username: "{{ netapp_username }}"
        password: "{{ netapp_password }}"
        dest_hostname: "{{ netapp_dest_hostname }}"

    - name: vserver peer delete
      na_ontap_vserver_peer:
        state: absent
        peer_vserver: ansible2
        vserver: ansible
        hostname: "{{ netapp_hostname }}"
        username: "{{ netapp_username }}"
        password: "{{ netapp_password }}"

