=================================================================
na_elementsw_account - Manage Element Software Account Manager
=================================================================
New in version 2.6

========
Synopsis
========
Manage Element software accounts

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
| state                | Choices:            | Whether the specified account should     |
|                      |                     | exist or not.                            |
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
| src_access_group_id  |                     | Unique username for this account. (May   |
| (required)           |                     | be 1 to 64 characters in length).        |
+----------------------+---------------------+------------------------------------------+
| new_element_username |                     | New name for the user account.           | 
+----------------------+---------------------+------------------------------------------+
| initiator_secret     |                     | CHAP secret to use for the initiator.    |
|                      |                     | Should be 12-16 characters long and      |
|                      |                     | impenetrable. The CHAP initiator secrets |
|                      |                     | must be unique and cannot be the same as |
|                      |                     | the target CHAP secret. If not           |
|                      |                     | specified, a random secret is created.   |
+----------------------+---------------------+------------------------------------------+
| target_secret        |                     | CHAP secret to use for the target        |
|                      |                     | (mutual CHAP authentication). Should be  |
|                      |                     | 12-16 characters long and impenetrable.  |
|                      |                     | The CHAP target secrets must be unique   |
|                      |                     | and cannot be the same as the initiator  |
|                      |                     | CHAP secret. If not specified, a random  |
|                      |                     | secret is created.                       |
+----------------------+---------------------+------------------------------------------+
| account_id           |                     | The ID of the account to manage or       |
|                      |                     | update.                                  |
+----------------------+---------------------+------------------------------------------+
| attributes           |                     | List of Name/Value pairs in JSON object  |
|                      |                     | format.                                  |
+----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples:

    - name: Create Account
      na_elementsw_account:
        hostname: "{{ elementsw_hostname }}"
        username: "{{ elementsw_username }}"
        password: "{{ elementsw_password }}"
        state: present
        element_username: TenantA

    - name: Modify Account
      na_elementsw_account:
        hostname: "{{ elementsw_hostname }}"
        username: "{{ elementsw_username }}"
        password: "{{ elementsw_password }}"
        state: present
        element_username: TenantA
        new_element_username: TenantA-Renamed

    - name: Delete Account
      na_elementsw_account:
        hostname: "{{ elementsw_hostname }}"
        username: "{{ elementsw_username }}"
        password: "{{ elementsw_password }}"
        state: absent
        element_username: TenantA-Renamed
