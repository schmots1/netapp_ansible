====================================================
na_ontap_dns - Manage NetApp ONTAP DNS.
====================================================
New in version 2.6

========
Synopsis
========
Create, delete, modify DNS servers.

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
| state           | Choices:            | Whether the specified dns servers should |
|                 |                     | be enabled for the specified vserver or  |
|                 | * present (default) | not.                                     |
|                 | * absent            |                                          |
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
| domains         |                     | List of DNS domains such as              |
|                 |                     | 'sales.bar.com'. The first domain is the |
|                 |                     | one that the Vserver belongs to.         |
+-----------------+---------------------+------------------------------------------+
| nameservers     |                     | List of IPv4 addresses of name servers   |
|                 |                     | such as '123.123.123.123'.               |
+-----------------+---------------------+------------------------------------------+
| vserver         |                     | The name of the vserver to use.          |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

- name: create DNS
      na_ontap_dns:
        state: present
        hostname: "{{hostname}}"
        username: "{{username}}"
        password: "{{password}}"
        vserver:  "{{vservername}}"
        domains: sales.bar.com
        nameservers: 10.193.0.250,10.192.0.250
