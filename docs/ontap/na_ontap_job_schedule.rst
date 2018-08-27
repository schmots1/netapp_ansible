======================================================
na_ontap_job_schedule - Manage NetApp ONTAP schedules.
======================================================
New in version 2.5.

========
Synopsis
========
Create, delete or modify job schedules on ONTAP

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
| hostname        |                     | The hostname or IP address of the ONTAP  |
| (required)      |                     | instance.                                |
+-----------------+---------------------+------------------------------------------+
| https           | Default: false      | Enable and disable https                 |
+-----------------+---------------------+------------------------------------------+
| validate_certs  | Default: true       | Set to false in order to use self-signed |
|                 |                     | certificates with https.  *Warning: this |
|                 |                     | does open up the small possiblity of a   |
|                 |                     | man-in-the-middle attack.                |
+-----------------+---------------------+------------------------------------------+
| job_minutes     |                     | The minute(s) of each hour when the job  |
|                 |                     | should be run. Job Manager cron          |
|                 |                     | scheduling minute. -1 represents all     |
|                 |                     | minutes and only supported for cron      |
|                 |                     | schedule create and modify.  Range is    |
|                 |                     | [-1.59]                                  |
+-----------------+---------------------+------------------------------------------+
| name            |                     | The name of the aggregate to manage.     |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| password        |                     | Password for the specified user.         |
| (required)      |                     |                                          |
+-----------------+---------------------+------------------------------------------+
| state           | Choices:            | Whether the specified aggregate should   |
|                 |                     | exist or not.                            |
|                 | * present (default) |                                          |
|                 | * absent            |                                          |
+-----------------+---------------------+------------------------------------------+
| username        |                     | This can be a Cluster-scoped or          |
| (required)      |                     | SVM-scoped account, depending on whether |
|                 |                     | a Cluster-level or SVM-level API is      |
|                 |                     | required. For more information, please   |
|                 |                     | read the documentation                   |
|                 |                     | https://goo.gl/BRu78Z.                   |
+-----------------+---------------------+------------------------------------------+

Notes

The modules prefixed with na_ontap are built to support the ONTAP storage platform.
Examples::

 - name: Create Job
   na_ontap_job_schedule:
     state: present
     name: jobName
     job_minutes: jobMinutes
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
 - name: Delete Job
   na_ontap_job_schedule:
     action: present
     name: jobName
     hostname: "{{ netapp_hostname }}"
     username: "{{ netapp_username }}"
     password: "{{ netapp_password }}"
