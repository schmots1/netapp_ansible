====================================================
na_ontap_svm - Manage NetApp ONTAP SVMs
====================================================
New in version 2.5.

========
Synopsis
========
Create, modify or delete SVMs on NetApp ONTAP

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

+-----------------------+---------------------+------------------------------------------+
|   Parameter           |   Choices/Defaults  |                 Comments                 |
+-----------------------+---------------------+------------------------------------------+
| aggr_list             |                     | List of aggregates assigned for volume   |
|                       |                     | operations. These aggregates could be    |
|                       |                     | shared for use with other Vservers. When |
|                       |                     | specified as part of a vserver-create,   |
|                       |                     | this field represents the list of        |
|                       |                     | aggregates that are assigned to the      |
|                       |                     | Vserver for volume operations. When part |
|                       |                     | of vserver-get-iter call, this will      |
|                       |                     | return the list of Vservers which have   |
|                       |                     | any of the aggregates specified as part  | 
|                       |                     | of the aggr-list.                        |
+-----------------------+---------------------+------------------------------------------+
| allowed_protocols     | Choices:            | When specified as part of a vserver-     |
|                       |                     | create, this field represent the list of |
|                       | * nfs               |  protocols allowed on the Vserver.       |
|                       | * cifs              |                                          |
|                       | * fcp               |                                          |
|                       | * iscs              |                                          |
|                       | * ndmp              |                                          |
|                       | * http              |                                          |
|                       | * nvme              |                                          |
+-----------------------+---------------------+------------------------------------------+
| hostname              |                     | The hostname or IP address of the ONTAP  |
| (required)            |                     | instance.                                |
+-----------------------+---------------------+------------------------------------------+
| https                 | Default: false      | Enable and disable https                 |
+-----------------------+---------------------+------------------------------------------+
| name                  |                     | The name of the SVM to manage.           |
| (required)            |                     |                                          |
+-----------------------+---------------------+------------------------------------------+
| new_name              |                     | The name of the SVM to be renamed        |
+-----------------------+---------------------+------------------------------------------+
| password              |                     | Password for the specified user.         |
| (required)            |                     |                                          |
+-----------------------+---------------------+------------------------------------------+
| root_volume           |                     | Root volume of the SVM.  Required when   |
|                       |                     | state=present                            |
+-----------------------+---------------------+------------------------------------------+
| root_volume_aggregate |                     | The aggregate on which the root volume   |
|                       |                     | will be create.  Required when           |
|                       |                     | state=present                            |
+-----------------------+---------------------+------------------------------------------+
| root_volume_secuirty_ | Choices:            | Security style of the root volume        |
| style                 |                     | Required when state=present              |
|                       | * unix              |                                          |
|                       | * ntfs              |                                          |
|                       | * mixed             |                                          |
|                       | * unified           |                                          |
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

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create SVM
   na_ontap_svm:
     state: present
     name: ansibleVServer
     root_volume: vol1
     root_volume_aggregate: aggr1
     root_volume_security_style: mixed
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

