=================================================================
na_elementsw_drive - Manage Element Software Node Drives
=================================================================
New in version 2.6

========
Synopsis
========
Add, Erase or Remove drive for nodes on Element Software Cluster.

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

+-----------------------+---------------------+------------------------------------------+
|     Parameter         |   Choices/Defaults  |                 Comments                 |
+-----------------------+---------------------+------------------------------------------+
| state                 | Choices:            | Whether the specified access group       |
|                       |                     | should exist or not                      |
|                       | * present           |                                          |
|                       | * absent            |                                          |
|                       | * clean             |                                          |
+-----------------------+---------------------+------------------------------------------+
| hostname              |                     | The hostname or IP address of the        |
| (required)            |                     | cluster mvip.                            |
+-----------------------+---------------------+------------------------------------------+
| username              |                     | Admin account username.                  |
| (required)            |                     |                                          |
+-----------------------+---------------------+------------------------------------------+
| password              |                     | Password for the specified username.     |
| (required)            |                     |                                          |
+-----------------------+---------------------+------------------------------------------+
| drive_id              |                     | Unique username for this account. (May   |
+-----------------------+---------------------+------------------------------------------+
| node_id               |                     | The password for the new admin account.  |
+-----------------------+---------------------+------------------------------------------+
| force_during_upgrade  |                     | Boolean, true for accepting Eula, False  |
+-----------------------+---------------------+------------------------------------------+
| force_during_bin_sync |                     | A list of types the admin has access to  |
+-----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

    - name: Add admin user
      na_elementsw_admin_users:
        state: present
        username: "{{ admin_user_name }}"
        password: "{{ admin_password }}"
        hostname: "{{ hostname }}"
        element_username: carchi8py
        element_password: carchi8py
        acceptEula: True
        access: accounts,drives

    - name: modify admin user
      na_elementsw_admin_users:
        state: present
        username: "{{ admin_user_name }}"
        password: "{{ admin_password }}"
        hostname: "{{ hostname }}"
        element_username: carchi8py
        element_password: carchi8py12
        acceptEula: True
        access: accounts,drives,nodes

    - name: delete admin user
      na_elementsw_admin_users:
        state: absent
        username: "{{ admin_user_name }}"
        password: "{{ admin_password }}"
        hostname: "{{ hostname }}"
        element_username: carchi8py
