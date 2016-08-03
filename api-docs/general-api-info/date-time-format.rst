.. _barbican-dg-date-time-format:

Date and time format
~~~~~~~~~~~~~~~~~~~~~

For the display and consumption of date and time values, Rackspace Cloud
services use a date format that complies with ISO 8601.

|product name| assumes that all times are given in UTC, and does not make
use of UTC offsets for time zones.

**Example: |product name| date and time format**

.. code::

    yyyy-MM-ddTHH:mm:ss

For example, the UTC format for May 19, 2016 at 8:07:08 a.m. is

.. code::

    2016-05-19T08:07:08

**Date and time format codes**

+------+-----------------------------------------------------------+
| yyyy | Four digit year                                           |
+======+===========================================================+
| MM   | Two digit month                                           |
+------+-----------------------------------------------------------+
| DD   | Two digit day                                             |
+------+-----------------------------------------------------------+
| T    | Separator for date/time                                   |
+------+-----------------------------------------------------------+
| HH   | Two digit hour (00-23)                                    |
+------+-----------------------------------------------------------+
| mm   | Two digit minute                                          |
+------+-----------------------------------------------------------+
| ss   | Two digit second                                          |
+------+-----------------------------------------------------------+
| Z    | (optional) UTC (Zulu) time designation.                   |
+------+-----------------------------------------------------------+
