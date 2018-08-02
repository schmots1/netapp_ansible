============================================
na_ontap_nterface - ONTAP LIF configuration.
============================================
New in version 2.5.

========
Synopsis
========
Create, delete and modify LIFs

============
Requirements
============
The below requirements are needed on the host that executes this module.

* A Data ONTAP system. The modules were developed with Clustered Data ONTAP 9.3
* Ansible 2.4
* netapp-lib (2017.10.30). Install using 'pip install netapp-lib'

==========
Parameters
==========

+-----------------------+---------------------+------------------------------------------+
|   Parameter           |   Choices/Defaults  |                 Comments                 |
+-----------------------+---------------------+------------------------------------------+
| address               |                     | Specifies the LIF's IP address. Required |
|                       |                     | when state=present                       |
+-----------------------+---------------------+------------------------------------------+
| administrative-status |                     | Specifies the administrative status of   |
|                       |                     | the LIF.                                 |
+-----------------------+---------------------+------------------------------------------+
| failover_policy       |                     | Specifies the failover policy for the LIF|
+-----------------------+---------------------+------------------------------------------+
| firewall_poilcy       |                     | Specifies the firewall policy for the LIF|
+-----------------------+---------------------+------------------------------------------+
| home_node             |                     | Specifies the LIF's home node. Required  |
|                       |                     | when state=present                       |
+-----------------------+---------------------+------------------------------------------+
| home_port             |                     | Specifies the LIF's home port. Required  |
|                       |                     | when state=present                       |
+-----------------------+---------------------+------------------------------------------+
| hostname              |                     | The hostname or IP address of the ONTAP  |
| (required)            |                     | instance.                                |
+-----------------------+---------------------+------------------------------------------+
| https                 | Default: false      | Enable and disable https                 |
+-----------------------+---------------------+------------------------------------------+
| interface_name        |                     | Specifies the logical interface (LIF)    |
| (required)            |                     | name                                     |
+-----------------------+---------------------+------------------------------------------+
| is_auto_revert        |                     | If true, data LIF will revert to its home|
|                       |                     | node under certain circumstances such as |
|                       |                     | startup, and load balancing migration    |
|                       |                     | capability is disabled automatically     |
+-----------------------+---------------------+------------------------------------------+
| netmask               |                     | Specifies the LIF's netmask. Required    |
|                       |                     | when state=present                       |
+-----------------------+---------------------+------------------------------------------+
| password              |                     | Password for the specified user.         |
| (required)            |                     |                                          |
+-----------------------+---------------------+------------------------------------------+
| protocols             | Choices             | Specifies the list of data protocols     |
|                       |                     | configured on the LIF.  By default, the  |
|                       | * none              | values in this element are nfs, cifs and |
|                       | * iscsi             | fcache. Other supported protocols are    |
|                       | * fcp               | iscsi and fcp.  A LIF can be configured  |
|                       |                     | to not support any data protocols by     |
|                       |                     | by specifying 'none'.                    |
+-----------------------+---------------------+------------------------------------------+
| state                 | Choices:            | Whether the specified aggregate should   |
|                       |                     | exist or not.                            |
|                       | * present (default) |                                          |
|                       | * absent            |                                          |
+-----------------------+---------------------+------------------------------------------+
| username              |                     | This can be a Cluster-scoped or          |
| (required)            |                     | SVM-scoped account, depending on whether |
|                       |                     | a Cluster-level or SVM-level API is      |
|                       |                     | required. For more information, please   |
|                       |                     | read the documentation                   |
|                       |                     | https://goo.gl/BRu78Z.                   |
+-----------------------+---------------------+------------------------------------------+
| vserver               |                     | The name of the SVM to use               |
| (required)            |                     |                                          |
+-----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create interface
   na_ontap_interface:
     state: present
     interface_name: data2
     home_port: e0d
     home_node: laurentn-vsim1
     role: data
     protocols: nfs
     admin_status: up
     failover_policy: local-only
     firewall_policy: mgmt
     is_auto_revert: true
     address: 10.10.10.10
     netmask: 255.255.255.0
     vserver: svm1
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: Delete interface
   na_ontap_interface:
     state: absent
     interface_name: data2
     vserver: svm1
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
