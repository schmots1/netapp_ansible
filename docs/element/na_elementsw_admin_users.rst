=================================================================
na_elementsw_admin_users - Manage Element Software Admin Users
=================================================================
New in version 2.6

========
Synopsis
========
Create, destroy, or update admin users on Element software

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

+----------------------+---------------------+------------------------------------------+
|     Parameter        |   Choices/Defaults  |                 Comments                 |
+----------------------+---------------------+------------------------------------------+
| state                | Choices:            | Whether the specified admin user should  |
|                      |                     | exist or not                             |
|                      | * present           |                                          |
|                      | * absent            |                                          |
+----------------------+---------------------+------------------------------------------+
| hostname             |                     | The hostname or IP address of the        |
| (required)           |                     | cluster mvip.                            |
+----------------------+---------------------+------------------------------------------+
| username             |                     | Admin account username.                  |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| password             |                     | Password for the specified username.     |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| element_username     |                     | Unique username for this account. (May   |
| (required)           |                     | be 1 to 64 characters in length).        |
+----------------------+---------------------+------------------------------------------+
| element_password     |                     | The password for the new admin account.  |
|                      |                     | Setting the password attribute will      |
|                      |                     | always reset your password, even if the  |
|                      |                     | password is the same.                    |
+----------------------+---------------------+------------------------------------------+
| acceptEula           |                     | Boolean, true for accepting Eula, False  |
|                      |                     | for rejecting Eula                       |
+----------------------+---------------------+------------------------------------------+
| access               |                     | A list of types the admin has access to  |
+----------------------+---------------------+------------------------------------------+

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
