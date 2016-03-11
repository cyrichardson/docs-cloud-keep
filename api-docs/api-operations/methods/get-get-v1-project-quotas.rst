
.. _get-project-quotas:

Get project quotas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/quotas

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


This request does not accept URI or body parameters.


**Example: Get project quotas cURL request**


.. code::

   curl -H 'Accept: application/json' -H 'X-Auth-Token:$AUTH_TOKEN'\
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
|**cas**       |         | for the CAs resource.                                        |
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

    {
      "quotas": {
        "secrets": 1000,
        "cas": 0,
        "orders": 0,
        "containers": 1000,
        "consumers": 1000
      }
    }
