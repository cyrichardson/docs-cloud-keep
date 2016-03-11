
.. _get-project-quotas:

Get project quotas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/{tenantId}/quotas

Get the effective quotas for the project of the requester. The project id
of the requester is derived from the authentication token provided in the
X-Auth-Token header.


The following table shows the possible response codes for this operation:


+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 200  | Successful Request                                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""


The following table shows the URI parameter for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{tenantId}                |String *(Required)*      |This parameter specifies |
|                          |                         |the tenant ID of the     |
|                          |                         |client subscribing to    |
|                          |                         |the Cloud Keep service.  |
+--------------------------+-------------------------+-------------------------+


This operation does not accept a request body.


**Example: Get project quotas cURL request**


.. code::

   curl -H 'Accept: application/json' \
        -H 'X-Auth-Token:$AUTH-TOKEN'\
        $ENDPOINT/v1/quotas


Response
""""""""""""""""

The following table shows the response attributes for this request.

+--------------+---------+--------------------------------------------------------------+
| Name         | Type    | Description                                                  |
+==============+=========+==============================================================+
|**quotas**    | dict    | Returns a dictionary with quota information                  |
+--------------+---------+--------------------------------------------------------------+
|quotas.\      | integer | Returns the effective quota value of the current project     |
|**secrets**   |         | for the secret resource.                                     |
+--------------+---------+--------------------------------------------------------------+
|quotas.\      | integer | Returns the effective quota value of the current project     |
|**orders**    |         | for the orders resource.                                     |
+--------------+---------+--------------------------------------------------------------+
|quotas.\      | integer | Returns the effective quota value of the current project     |
|**containers**|         | for the containers resource.                                 |
+--------------+---------+--------------------------------------------------------------+
|quotas.\      | integer | Returns the effective quota value of the current project     |
|**consumers** |         | for the consumers resource.                                  |
+--------------+---------+--------------------------------------------------------------+
|quotas.\      | integer | Returns the effective quota value of the current project     |
|**cas**       |         | for the CAs resource.                                        |
+--------------+---------+--------------------------------------------------------------+

Effective quota values are interpreted as follows:

+-------+-----------------------------------------------------------------------------+
| Value | Description                                                                 |
+=======+=============================================================================+
|  -1   | A negative value indicates the resource is unconstrained by a quota.        |
+-------+-----------------------------------------------------------------------------+
|   0   | A zero value indicates that the resource is disabled.                       |
+-------+-----------------------------------------------------------------------------+
| int   | A positive value indicates the maximum number of that resource that can be  |
|       | created for the current project.                                            |
+-------+-----------------------------------------------------------------------------+

**Example: Get project quotas HTTP header and JSON response**


.. code::

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
          "quotas": {
            "secrets": 10,
            "orders": 20,
            "containers": 10,
            "consumers": -1,
            "cas": 5
         }
       }
