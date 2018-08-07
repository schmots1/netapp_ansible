===========================================================================
na_elementsw_snapshot_schedule - Manage Element Software Snapshot Schedules
===========================================================================
New in version 2.6

========
Synopsis
========
Create, destroy, or update accounts on Element software.

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

+-------------------------+-------------------------+------------------------------------------+
|       Parameter         |     Choices/Defaults    |                 Comments                 |
+-------------------------+-------------------------+------------------------------------------+
| state                   | Choices:                | Whether the specified account should     |
|                         |                         | exist or not.                            |
|                         | * present               |                                          |
|                         | * absent                |                                          |
+-------------------------+-------------------------+------------------------------------------+
| hostname                |                         | The hostname or IP address of the        |
| (required)              |                         | cluster mvip.                            |
+-------------------------+-------------------------+------------------------------------------+
| username                |                         | Admin account username.                  |
| (required)              |                         |                                          |
+-------------------------+-------------------------+------------------------------------------+
| password                |                         | Password for the specified username.     |
| (required)              |                         |                                          |
+-------------------------+-------------------------+------------------------------------------+
| paused                  |                         | Pause / Resume a schedule.               |
+-------------------------+-------------------------+------------------------------------------+
| recurring               |                         | Should the schedule recur?               |
+-------------------------+-------------------------+------------------------------------------+
| schedule_type           | Choices:                | Schedule type for creating schedule.     |
|                         |                         |                                          |
|                         | * DaysOfWeekFrequency   |                                          |
|                         | * DaysOfMonthFrequency  |                                          |
|                         | * TimeIntervalFrequency |                                          |
+-------------------------+-------------------------+------------------------------------------+
| target_secret           |                         | CHAP secret to use for the target        |
+-------------------------+-------------------------+------------------------------------------+
| time_interval_days      | Default: 1              | Time interval in days.                   |
+-------------------------+-------------------------+------------------------------------------+
| time_interval_hours     | Default: 0              | Time interval in hours.                  |
+-------------------------+-------------------------+------------------------------------------+
| time_interval_minutes   | Default: 0              | Time interval in minutes.                |
+-------------------------+-------------------------+------------------------------------------+
| days_of_week_weekdays   |                         | List of days of the week (Sunday to      |
|                         |                         | Saturday)                                |
+-------------------------+-------------------------+------------------------------------------+
| days_of_week_hours      | Default: 0              | Time specified in hours.                 |
+-------------------------+-------------------------+------------------------------------------+
| days_of_week_minutes    | Default: 0              | Time specified in minutes.               |
+-------------------------+-------------------------+------------------------------------------+
| days_of_month_monthdays |                         | List of days of the month (1-31).        |
+-------------------------+-------------------------+------------------------------------------+
| days_of_month_hours     | Default: 0              | Time specified in hours.                 |
+-------------------------+-------------------------+------------------------------------------+
| days_of_month_minutes   | Default: 0              | Time specified in minutes.               |
+-------------------------+-------------------------+------------------------------------------+
| name                    |                         | Name for the snapshot schedule. It       |
|                         |                         | accepts either schedule_id or            |
|                         |                         | schedule_name. If name is digit, it will |
|                         |                         | consider as schedule_id. If name is      |
|                         |                         | string, it will consider as              |
|                         |                         | schedule_name.                           |
+-------------------------+-------------------------+------------------------------------------+
| snapshot_name           |                         | Name for the created snapshots.          |
+-------------------------+-------------------------+------------------------------------------+
| volumes                 |                         | Volume IDs that you want to set the      |
|                         |                         | snapshot schedule for.                   |
+-------------------------+-------------------------+------------------------------------------+
|  account_id             |                         | Account ID for the owner of this volume. |
|                         |                         | It accepts either account_name or        |
|                         |                         | account_id.  If account_id is digit, it  |
|                         |                         | will consider as account_id. If          |
|                         |                         | account_id is string, it will consider   | 
|                         |                         | as account_name.                         |
+-------------------------+-------------------------+------------------------------------------+
| retention               |                         | Retention period for the snapshot.       |
|                         |                         | Format is 'HH:mm:ss'.                    |
+-------------------------+-------------------------+------------------------------------------+
| starting_date           |                         | Starting date for the schedule. Required |
|                         |                         | when state=present.                      |
|                         |                         | Format: 2016-12-01T00:00:00Z             |
+-------------------------+-------------------------+------------------------------------------+


Notes

The modules prefixed with na_elementsw are built to support the Element software platform.
Examples::

   - name: Create Snapshot schedule
     na_elementsw_snapshot_schedule:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: present
       name: Schedule_A
       schedule_type: TimeIntervalFrequency
       time_interval_days: 1
       starting_date: '2016-12-01T00:00:00Z'
       volumes:
       - 7
       - test
       account_id: 1

   - name: Update Snapshot schedule
     na_elementsw_snapshot_schedule:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: present
       name: Schedule_A
       schedule_type: TimeIntervalFrequency
       time_interval_days: 1
       starting_date: '2016-12-01T00:00:00Z'
       volumes:
       - 8
       - test1
       account_id: 1

   - name: Delete Snapshot schedule
     na_elementsw_snapshot_schedule:
       hostname: "{{ elementsw_hostname }}"
       username: "{{ elementsw_username }}"
       password: "{{ elementsw_password }}"
       state: absent
       name: 6
