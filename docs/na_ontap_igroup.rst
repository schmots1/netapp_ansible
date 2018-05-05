=============================================
na_ontap_igroup - ONTAP igroup configuration.
=============================================
New in version 2.5.

========
Synopsis
========
Create, destroy and manage Igroups including initiators.

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

+----------------------+---------------------+------------------------------------------+
|   Parameter          |   Choices/Defaults  |                 Comments                 |
+----------------------+---------------------+------------------------------------------+
| bind_portset         |                     | Name of a current portset to bind to the |
|                      |                     | newly created igroup.                    |
+----------------------+---------------------+------------------------------------------+
| force                |                     | Forcibly remove the initator even if     |
|                      |                     | there are existing LUNSs mapped to this  |
|                      |                     | initiator group.                         |
+----------------------+---------------------+------------------------------------------+
| hostname             |                     | The hostname or IP address of the ONTAP  |
| (required)           |                     | instance.                                |
+----------------------+---------------------+------------------------------------------+
| https                | Default: false      | Enable and disable https                 |
+----------------------+---------------------+------------------------------------------+
| initiator            |                     | WWPN, WWPN Alias, or iSCSI name of       |
|                      |                     | Initiator to add or remove.              |
+----------------------+---------------------+------------------------------------------+
| initiator_group_type | Choices             | Type of the initiator group.  Required   |
|                      |                     | when state=present                       |
|                      | * fcp               |                                          |
|                      | * iscsi             |                                          |
|                      | * mixed             |                                          |
+----------------------+---------------------+------------------------------------------+
| name                 |                     | The name of the aggregate to manage.     |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| password             |                     | Password for the specified user.         |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| rename               |                     | The name of the aggregate that replaces  |
|                      |                     | the current name.                        |
+----------------------+---------------------+------------------------------------------+
| service_state        | Choices:            | Whether the specified aggregate should be|
|                      |                     | enabled or disabled. Creates aggregate if|
|                      | * online            | it doesn't exist.                        |
|                      | * offline           |                                          |
+----------------------+---------------------+------------------------------------------+
| state                | Choices:            | Whether the specified aggregate should   |
|                      |                     | exist or not.                            |
|                      | * present (default) |                                          |
|                      | * absent            |                                          |
+----------------------+---------------------+------------------------------------------+
| unmount_volumes      | Choices:            | If set to "TRUE", this option specifies  |
|                      |                     | that all of the volumes hosted by the    |
|                      | * true              | given aggregate are to be unmounted      |
|                      | * false             | before the offline operation is executed.|
|                      |                     | By default, the system will reject any   |
|                      |                     | attempt to offline an aggregate that     | 
|                      |                     | hosts one or more online volumes.        |
+----------------------+---------------------+------------------------------------------+
| username             |                     | This can be a Cluster-scoped or          |
| (required)           |                     | SVM-scoped account, depending on whether |
|                      |                     | a Cluster-level or SVM-level API is      |
|                      |                     | required. For more information, please   |
|                      |                     | read the documentation                   |
|                      |                     | https://goo.gl/BRu78Z.                   |
+----------------------+---------------------+------------------------------------------+
| vserver              |                     | The name of the SVM to use.              |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create Igroup
   na_ontap_igroup:
     state: present
     name: ansibleIgroup3
     initiator-group-type: iscsi
     ostype: linux
     initiator: iqn.1994-05.com.redhat:scspa0395855001.rtp.openenglab.netapp.com
     vserver: ansibleVServer
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: rename Igroup
   na_ontap_igroup:
     state: absent
     name: ansibleIgroup3
     initiator-group-type: iscsi
     ostype: linux
     initiator: iqn.1994-05.com.redhat:scspa0395855001.rtp.openenglab.netapp.com
     vserver: ansibleVServer
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: remove Igroup
   na_ontap_igroup:
     state: absent
     name: ansibleIgroup3
     initiator-group-type: iscsi
     ostype: linux
     initiator: iqn.1994-05.com.redhat:scspa0395855001.rtp.openenglab.netapp.com
     vserver: ansibleVServer
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
