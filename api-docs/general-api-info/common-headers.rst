.. _barbican-dg-common-headers:

Common headers
^^^^^^^^^^^^^^^^

The following table describes the common headers used by the API.

**Table: Common headers**

+-----------------------+----------------------------------------------------+
| Header                | Description                                        |
+=======================+====================================================+
| X-Auth-Token          | Authentication token. Required.                    |
+-----------------------+----------------------------------------------------+
| X-Project-Id          | A unique ID for the user to which the value of     |
|                       | ``X-Auth-Token`` grants access. The unique ID is   |
|                       | your account ID.                                   |
+-----------------------+----------------------------------------------------+
| Accept                | Media type. Initially, only text and binary types  |
|                       | are supported.                                     |
+-----------------------+----------------------------------------------------+
| Accept-Encoding       | Specifies that the agent accepts gzip-encoded      |
|                       | response bodies                                    |
+-----------------------+----------------------------------------------------+
| Content-Length        | For **POST** or **PUT** requests, the length in    |
|                       | bytes of the message document being submitted      |
+-----------------------+----------------------------------------------------+
| Content-Type          | ``application/json``                               |
+-----------------------+----------------------------------------------------+
| Date                  | Current date and time                              |
+-----------------------+----------------------------------------------------+
| Host                  | Host name of the API                               |
+-----------------------+----------------------------------------------------+
