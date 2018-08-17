=======================================================
na_ontap_autosupport - Manage NetApp ONTAP autosupport.
=======================================================
New in version 2.6

========
Synopsis
========
Enable or disabled autosupport on NetApp ONTAP.

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
| state           | Choices:            | Specifies whether the AutoSupport daemon |
|                 |                     | is present or absent.  When this setting |
|                 | * present (default) | is absent, delivery of all AutoSupport   |
|                 | * absent            | sages is turned off.                     |
+-----------------+---------------------+------------------------------------------+
| hostname        |                     | The hostname or IP address of the ONTAP  |
| (required)      |                     | instance.                                |
+-----------------+---------------------+------------------------------------------+
| username        |                     | This can be a Cluster-scoped or          |
| (required)      |                     | SVM-scoped account, depending on whether |
|                 |                     | a Cluster-level or SVM-level API is      |
|                 |                     | required. For more information, please   |
|                 |                     | read the documentation                   |
|                 |                     | https://goo.gl/BRu78Z.                   |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| https           | Default: false      | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| validate_certs  | Default: true       | Set to false in order to use self-signed |
|                 |                     | certificates with https.  *Warning: this |
|                 |                     | does open up the small possiblity of a   |
|                 |                     | man-in-the-middle attack.                |
+-----------------+---------------------+------------------------------------------+
| mail_hosts      |                     | List of mail server(s) used to deliver   |
|                 |                     | AutoSupport messages via SMTP. Both host |
|                 |                     | names and IP addresses may be used as    |
|                 |                     | valid input. One can optionally specify  |
|                 |                     | a username/password for authentication   |
|                 |                     | with the mail server.                    |
+-----------------+---------------------+------------------------------------------+
| node_name       |                     | The name fo the filer that owns the      |
|                 |                     | AutoSupport Configuration.               |
+-----------------+---------------------+------------------------------------------+
| noteto          |                     | Specifies up to five recipients of full  |
|                 |                     | AutoSupport e-mail messages.             |
+-----------------+---------------------+------------------------------------------+
| post_url        |                     | The URL used to deliver AutoSupport      |
|                 |                     | messages via HTTP POST.                  |
+-----------------+---------------------+------------------------------------------+
| support         |                     | Specifies whether AutoSupport            |
|                 |                     | notification to technical support is     |
|                 |                     | enabled.                                 |
+-----------------+---------------------+------------------------------------------+
| transpoprt      | Choices:            | The name of the transport protocol used  |
|                 |                     | to deliver AutoSupport messages.         |
|                 | * http              |                                          |
|                 | * https             |                                          |
|                 | * smtp              |                                          |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

- name: Enable autosupport
     na_ontap_autosupport:
       hostname: "{{ hostname }}"
       username: "{{ username }}"
       password: "{{ password }}"
       state: present
       node_name: test
       transport: https
       noteto: abc@def.com,def@ghi.com
       mail_hosts: 1.2.3.4,5.6.7.8
       support: False
       post_url: url/1.0/post

   - name: Disable autosupport
     na_ontap_autosupport:
       hostname: "{{ hostname }}"
       username: "{{ username }}"
       password: "{{ password }}"
       state: absent
       node_name: test
