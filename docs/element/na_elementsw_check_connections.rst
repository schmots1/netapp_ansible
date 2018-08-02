====================================================================
na_elementsw_check_connections - Check Connectivity To MVIP And SVIP
====================================================================
New in version 2.6

========
Synopsis
========
Used to test the management connection to the cluster.
The test pings the MVIP and SVIP, and executes a simple API method to verify connectivity.

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
| hostname             |                     | The hostname or IP address of the        |
| (required)           |                     | cluster mvip.                            |
+----------------------+---------------------+------------------------------------------+
| username             |                     | Admin account username.                  |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| password             |                     | Password for the specified username.     |
| (required)           |                     |                                          |
+----------------------+---------------------+------------------------------------------+
| skip                 | Choices:            | Skip checking connection to SVIP or MVIP |
|                      |                     |                                          |
|                      | * svip              |                                          |
|                      | * mvip              |                                          |
+----------------------+---------------------+------------------------------------------+
| mvip                 |                     | Optionally, use to test connection of a  |
|                      |                     | different MVIP.This is not needed to     |
|                      |                     | test the connection to the target        |
|                      |                     | cluster.                                 |
+----------------------+---------------------+------------------------------------------+
| svip                 |                     | Optionally, use to test connection of a  |
|                      |                     | different SVIP.This is not needed to     |
|                      |                     | test the connection to the target        |
|                      |                     | cluster.                                 |
+----------------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

   - name: Check connections to MVIP and SVIP
     na_elementsw_check_connections:
       hostname: "{{ solidfire_hostname }}"
       username: "{{ solidfire_username }}"
       password: "{{ solidfire_password }}"
