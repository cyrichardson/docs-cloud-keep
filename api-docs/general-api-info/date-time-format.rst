.. _date-time-format:

====================
Date and time format
====================

The service uses an ISO 8601 compliant date format for the
display and consumption of date and time values. The system time is
expressed as UTC.

.. _datetime-loadbalance:

**Service date and time format**

.. code::

    YYYY-MM-DD'T'hh:mm:ssZ

For example, the UTC-5 format for May 19, 2016 at 8:07:08 AM, GMT-5 is as
follows:

.. code::

    2016-05-19T08:07:08-05:00

The following table describes the date and time format codes.

.. _datetime-codes:

.. list-table:: **Date and time format codes**
   :widths: 20 50
   :header-rows: 1

   * - Code
     - Description
   * - YYYY
     - Four-digit year
   * - MM
     - Two-digit month
   * - DD
     - Two-digit day
   * - T
     - Separator for the date and time
   * - hh
     - Two-digit hour (00-23)
   * - mm
     - Two-digit minute
   * - ss
     - Two-digit second
   * - Z
     - RFC 822 time zone (offset from GMT) If Z is not replaced with the
       offset from UTC, it indicates a 00:00 offset.
