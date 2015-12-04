
.. _put-configured-project-quotas:

Update configured project quotas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/{tenantId}/project-quotas/{uuid}


Create or update the configured project quotas for the project with the specified UUID.



This table shows the possible response codes for this operation:


+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 204  | Successful request                                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 404  | Not Found                                                                   |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""


This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{tenantId}                |String *(Required)*      |This parameter specifies |
|                          |                         |the tenant ID of the     |
|                          |                         |client subscribing to    |
|                          |                         |the Cloud Keep service.  |
+--------------------------+-------------------------+-------------------------+
|{uuid}                    |String *(Required)*      |This parameter specifies |
|                          |                         |the UUID for the         |
|                          |                         |specified project.       |
+--------------------------+-------------------------+-------------------------+

This table shows the parameters for the request:

Request Attributes
******************

+----------------+---------+----------------------------------------------+
| Attribute Name | Type    | Description                                  |
+================+=========+==============================================+
| project-quotas | dict    | A dictionary with project quota information. |
+----------------+---------+----------------------------------------------+
| secrets        | integer | The value to set for this project's secret   |
|                |         | quota.                                       |
+----------------+---------+----------------------------------------------+
| orders         | integer | The value to set for this project's order    |
|                |         | quota.                                       |
+----------------+---------+----------------------------------------------+
| containers     | integer | The value to set for this project's          |
|                |         | container quota.                             |
+----------------+---------+----------------------------------------------+
| consumers      | integer | The value to set for this project's          |
|                |         | consumer quota.                              |
+----------------+---------+----------------------------------------------+
| cas            | integer | The value to set for this project's          |
|                |         | CA quota.                                    |
+----------------+---------+----------------------------------------------+

Configured project quota values are specified as follows:

+-------+-----------------------------------------------------------------------------+
| Value | Description                                                                 |
+=======+=============================================================================+
|  -1   | A negative value indicates the resource is unconstrained by a quota.        |
+-------+-----------------------------------------------------------------------------+
|   0   | A zero value indicates that the resource is disabled.                       |
+-------+-----------------------------------------------------------------------------+
| int   | A positive value indicates the maximum number of that resource that can be  |
|       | created for the specified project.                                          |
+-------+-----------------------------------------------------------------------------+
|       | If a value is not given for a resource, this indicates that the default     |
|       | quota should be used for that resource for the specified project.           |
+-------+-----------------------------------------------------------------------------+

**Example update project quotas: JSON request**


.. code::

      curl -s https://endpointURL/v1/12345/project-quotas/{uuid} \
      -X PUT \
      -d '{
            "project_quotas": {
                "secrets": 50,
                "orders": 10,
                "containers": 20
            }
          }
          ' \
          -H 'X-Auth-Token: your_auth_token' \
          -H 'Content-Type: application/json'


Response
""""""""""""""""

This request does not return a response body.
