.. _response-codes:

==============
Response codes
==============

The |product name| REST API returns an HTTP response code that denotes the
success or failure of the operation.

-  Successful response codes are returned only if all configured
   providers were successful in processing the request.

-  Error response codes are accompanied by an ``application/json``
   response body that contains the error messages.

This API uses `standard HTTP 1.1 response codes`_.

.. _standard HTTP 1.1 response codes: http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html

The following table lists possible responses with their associated codes
and descriptions.


**Table: List of common response codes**

+---------------------+---------------+-----------------------------------------+
|     Response        | Associated    | Description                             |
|                     | response code |                                         |
+=====================+===============+=========================================+
| OK                  | 200           | The request to retrieve a resource      |
|                     |               | was successful.                         |
+---------------------+---------------+-----------------------------------------+
| Created             | 201           | The request to create a resource was    |
|                     |               | successful.                             |
+---------------------+---------------+-----------------------------------------+
| Accepted            | 202           | The request was accepted for            |
|                     |               | asynchronous processing.                |
+---------------------+---------------+-----------------------------------------+
| No Content          | 204           | The request has was successful and      |
|                     |               | the service did not return any content. |
|                     |               | For example, a successful DELETE        |
|                     |               | operations returns this code.           |
+---------------------+---------------+-----------------------------------------+
| Bad Request         | 400           | The request was not processed because   |
|                     |               | of an error in the input values.        |
|                     |               | Recheck the parameters to the service   |
|                     |               | and resubmit.                           |
+---------------------+---------------+-----------------------------------------+
| Unauthorized        | 401           | The request was not processed because   |
|                     |               | of an authentication failure.  This     |
|                     |               | response is often the result of a bad   |
|                     |               | user ID, password, or authentication    |
|                     |               | token.                                  |
+---------------------+---------------+-----------------------------------------+
| Forbidden           | 403           | The request was not processed because   |
|                     |               | of an authorization failure. Check that |
|                     |               | your service catalog contains the Cloud |
|                     |               | Keep endpoint and that your user has    |
|                     |               | the correct role-based access control   |
|                     |               | (RBAC) roles.                           |
+---------------------+---------------+-----------------------------------------+
| Service Unavailable | 503           | The service is currently unavailable.   |
|                     |               | For example, it might be offline for    |
|                     |               | scheduled platform maintenance. Try     |
|                     |               | again later.                            |
+---------------------+---------------+-----------------------------------------+

 
**Example: Error message**

.. code::

    HTTP/1.1 400 Bad Request
    Content-Type: application/json

    {
        "code": 400,
        "description": "Malformed JSON",
        "title": "Bad Request"
    }
