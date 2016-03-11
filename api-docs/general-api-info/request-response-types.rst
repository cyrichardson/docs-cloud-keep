.. _barbican-dg-request-response-types:

Request and response types
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The |product name| API supports JSON data serialization
formats.

**Response Format**

+----------+---------------------+----------------------+---------+
| Format   | Accept Header       | Query Extension      | Default |
+==========+=====================+======================+=========+
| JSON     | application/json    | .json                | Yes     |
+----------+---------------------+----------------------+---------+


Specify the request format by using the ``Content-Type`` header, which
is required for operations that have a request body.

You can specify the response format in requests by using the ``Accept``
header. If no response format is specified, JSON is the default
response format.
