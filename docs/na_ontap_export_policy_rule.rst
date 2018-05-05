=======================================================================
na_ontap_export_policy_rule - Manage NetApp ONTAP export policy rules.
=======================================================================
New in version 2.5.

========
Synopsis
========
Create, delete or rename export policy rules in ONTAP

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

+---------------------+---------------------+------------------------------------------+
|   Parameter         |   Choices/Defaults  |                 Comments                 |
+---------------------+---------------------+------------------------------------------+
| allow_suid          | Choices:            | If 'true', NFS server will honor SetUID  |
|                     |                     | bits in SETATTR operation.  Default value|
|                     | * yes               | is 'yes'                                 |
|                     | * no                |                                          |
+---------------------+---------------------+------------------------------------------+
| client_match        |                     | List of Client Match Hostnames, IP       |
|                     |                     | Addresses, Netgroups, or Domains         |
+---------------------+---------------------+------------------------------------------+
| hostname            |                     | The hostname or IP address of the ONTAP  |
| (required)          |                     | instance.                                |
+---------------------+---------------------+------------------------------------------+
| https               | Default: false      | Enable and disable https                 |
+---------------------+---------------------+------------------------------------------+
| password            |                     | Password for the specified user.         |
| (required)          |                     |                                          |
+---------------------+---------------------+------------------------------------------+
| policy_name         |                     | The name of the export policy the rule is|
| (required)          |                     | a part of.                               |
+---------------------+---------------------+------------------------------------------+
| protocol            | Choices:            | Client access protocol. Default value is |
|                     |                     | 'any'                                    |
|                     | * any               |                                          |
|                     | * nfs               |                                          |
|                     | * nfs3              |                                          |
|                     | * nfs4              |                                          |
|                     | * cifs              |                                          |
|                     | * flexcache         |                                          |
+---------------------+---------------------+------------------------------------------+
| ro_rule             | Choices:            | Read only access specifications for the  |
|                     |                     | rule.                                    |
|                     | * any               |                                          |
|                     | * none              |                                          |
|                     | * never             |                                          |
|                     | * krb5              |                                          |
|                     | * krb5i             |                                          |
|                     | * krb5p             |                                          |
|                     | * ntlm              |                                          |
|                     | * sys               |                                          |
+---------------------+---------------------+------------------------------------------+
| rw_rule             | Choices:            | Read Write access specifications for the |
|                     |                     | rule.                                    |
|                     | * any               |                                          |
|                     | * none              |                                          |
|                     | * never             |                                          |
|                     | * krb5              |                                          |
|                     | * krb5i             |                                          |
|                     | * krb5p             |                                          |
|                     | * ntlm              |                                          |
|                     | * sys               |                                          |
+---------------------+---------------------+------------------------------------------+
| state               | Choices:            | Whether the specified aggregate should   |
|                     |                     | exist or not.                            |
|                     | * present (default) |                                          |
|                     | * absent            |                                          |
+---------------------+---------------------+------------------------------------------+
| super_user_security | Choices:            | Read Write access specifications for the |
|                     |                     | rule.                                    |
|                     | * any               |                                          |
|                     | * none              |                                          |
|                     | * never             |                                          |
|                     | * krb5              |                                          |
|                     | * krb5i             |                                          |
|                     | * krb5p             |                                          |
|                     | * ntlm              |                                          |
|                     | * sys               |                                          |
+---------------------+---------------------+------------------------------------------+
| username            |                     | This can be a Cluster-scoped or          |
| (required)          |                     | SVM-scoped account, depending on whether |
|                     |                     | a Cluster-level or SVM-level API is      |
|                     |                     | required. For more information, please   |
|                     |                     | read the documentation                   |
|                     |                     | https://goo.gl/BRu78Z.                   |
+---------------------+---------------------+------------------------------------------+
| vserver             |                     | Name of the SVM to use.                  |
+---------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create ExportPolicyRule
   na_ontap_export_policy_rule:
     state: present
     policy_name: default123
     vserver: ci_dev
     client_match: 0.0.0.0/0
     ro_rule: any
     rw_rule: any
     protocol: any
     super_user_security: any
     allow_suid: true
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

 - name: Delete ExportPolicyRule
   na_ontap_volume:
     state: absent
     policy_name: default123
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
 
 - name: Modify ExportPolicyRule
   na_ontap_export_policy_rule:
     state: present
     policy_name: default123
     client_match: 0.0.0.0/0
     ro_rule: any
     rw_rule: any
     super_user_security: none
     protocol: any
     allow_suid: false
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"

