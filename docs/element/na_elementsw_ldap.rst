=================================================================
na_element_ldap - Manage Element Software LDAP Admin Users
=================================================================
New in version 2.6

========
Synopsis
========
Enable, disable ldap, and add ldap users

============
Requirements
============
The below requirements are needed on the host that executes this module.

* An Element software system.  Tested with Element OS 10
* Ansible 2.4 or higher
* solidfire-sdk-python (1.5.0.87). Install using 'pip install solidfire-sdk-python'

==========
Parameters
==========

+-------------------------+---------------------+------------------------------------------+
|       Parameter         |   Choices/Defaults  |                 Comments                 |
+-------------------------+---------------------+------------------------------------------+
| state                   | Choices:            | Whether the specified ldap element       |
|                         |                     | should exist or not.                     |
|                         | * present           |                                          |
|                         | * absent            |                                          |
+-------------------------+---------------------+------------------------------------------+
| hostname                |                     | The hostname or IP address of the        |
| (required)              |                     | cluster mvip.                            |
+-------------------------+---------------------+------------------------------------------+
| username                |                     | Admin account username.                  |
| (required)              |                     |                                          |
+-------------------------+---------------------+------------------------------------------+
| password                |                     | Password for the specified username.     |
| (required)              |                     |                                          |
+-------------------------+---------------------+------------------------------------------+
| authType                | Choices:            | Identifies which user authentication     |
|                         |                     | method to use.                           |
|                         | * DirectBind        |                                          |
|                         | * SearchAndBind     |                                          |
+-------------------------+---------------------+------------------------------------------+
| groupSearchBaseDn       |                     | he base DN of the tree to start the      |
|                         |                     | group search (will do a subtree search   |
|                         |                     | from here).                              |
+-------------------------+---------------------+------------------------------------------+
| groupSearchType         | Choices:            | Controls the default group search filter |
|                         |                     | used.                                    |
|                         | * NoGroup           |                                          |
|                         | * ActiveDirectory   |                                          |
|                         | * MemberDN          |                                          |
+-------------------------+---------------------+------------------------------------------+
| serverURIs              |                     | A comma-separated list of LDAP server    |
|                         |                     | URIs.                                    |
+-------------------------+---------------------+------------------------------------------+
| userSearchBaseDN        |                     | The base DN of the tree to start the     |
|                         |                     | search (will do a subtree search from    |
|                         |                     | here).                                   |
+-------------------------+---------------------+------------------------------------------+
| searchBindDN            |                     | A dully qualified DN to log in with to   |
|                         |                     | perform an LDAp search for the user      |
|                         |                     | (needs read access to the LDAP           |
|                         |                     | directory).                              |
+-------------------------+---------------------+------------------------------------------+
| searchBindPassword      |                     | The password for the searchBindDN        |
|                         |                     | account used for searching.              |
+-------------------------+---------------------+------------------------------------------+
| userSearchFilter        |                     | The LDAP Filter to use                   |
+-------------------------+---------------------+------------------------------------------+
| userDNTemplate          |                     | A string that is used form a fully       |
|                         |                     | qualified user DN.                       |
+-------------------------+---------------------+------------------------------------------+
| groupSearchCustomFilter |                     | For use with the CustomFilter Search     |
|                         |                     | type.                                    |
+-------------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

    - name: disable ldap authentication
      na_elementsw_ldap:
        state: absent
        username: "{{ admin username }}"
        password: "{{ admin password }}"
        hostname: "{{ hostname }}"

    - name: Enable ldap authentication
      na_elementsw_ldap:
        state: present
        username: "{{ admin username }}"
        password: "{{ admin password }}"
        hostname: "{{ hostname }}"
        authType: DirectBind
        serverURIs: ldap://svmdurlabesx01spd_ldapclnt
        groupSearchType: MemberDN
        userDNTemplate:  uid=%USERNAME%,cn=users,cn=accounts,dc=corp,dc="{{ company name }}",dc=com
