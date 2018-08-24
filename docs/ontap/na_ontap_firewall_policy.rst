=================================================================
na_ontap_firewall_policy - Manage NetApp ONTAP Firewall Policies.
=================================================================
New in version 2.7

========
Synopsis
========
Manage a firewall policy for an ONTAP system

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
| state           | Choices:            | Whether to set up a firewall policy or   |
|                 |                     | not.                                     |
|                 | * present (default) |                                          |
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
| allow_list      |                     | A list of IPs and masks to use.          |
+-----------------+---------------------+------------------------------------------+
| enable          | Choices:            | Enable or disable firewall.              |
|                 |                     |                                          |
|                 | * enable            |                                          |
|                 | * disable           |                                          |
+-----------------+---------------------+------------------------------------------+
| logging         | Choices:            | Enable or disable logging.               |
|                 |                     |                                          |
|                 | * enable            |                                          |
|                 | * disable           |                                          |
+-----------------+---------------------+------------------------------------------+
| node            |                     | The node to run the firewall             |
| (required)      |                     | configuration on.                        |
+-----------------+---------------------+------------------------------------------+
| policy          |                     | A policy name for the firewall policy.   |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| service         | Choices:            | The service to apply the policy to.      |
| (required)      |                     |                                          |
|                 | * http              |                                          |
|                 | * https             |                                          |
|                 | * ntp               |                                          |
|                 | * rsh               |                                          |
|                 | * snmp              |                                          |
|                 | * ssh               |                                          |
|                 | * telnet            |                                          |
+-----------------+---------------------+------------------------------------------+
| vserver         |                     | The Vserver to apply the policy to.      |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

- name: create firewall Policy
      na_ontap_firewall_policy:
        state: present
        allow_list: [1.2.3.4/24,1.3.3.4/24]
        policy: pizza
        service: http
        vserver: ci_dev
        hostname: "{{ netapp hostname }}"
        username: "{{ netapp username }}"
        password: "{{ netapp password }}"
        node: laurentn-vsim1

    - name: Modify firewall Policy
      na_ontap_firewall_policy:
        state: present
    - name: Modify firewall Policy
      na_ontap_firewall_policy:
        state: present
        allow_list: [1.2.3.4/24,1.3.3.4/24]
        policy: pizza
        service: http
        vserver: ci_dev
        hostname: "{{ netapp hostname }}"
        username: "{{ netapp username }}"
        password: "{{ netapp password }}"
        node: laurentn-vsim1

    - name: Destory firewall Policy
      na_ontap_firewall_policy:
        state: absent
        policy: pizza
        service: http
        vserver: ci_dev
        hostname: "{{ netapp hostname }}"
        username: "{{ netapp username }}"
        password: "{{ netapp password }}"
        node: laurentn-vsim1
