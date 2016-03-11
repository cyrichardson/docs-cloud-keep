
.. _get-project-quota-details:

Get Project quota details
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v1/project-quotas/{uuid}

Retrieves a project's configured project quota information.

The following table shows the possible response codes for this operation:

+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 200  | Successful request                                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 404  | Not Found.  The requested project does not have any configured quotas.      |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""

The following table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{tenantId}                |String *(Required)*      |This parameter specifies |
|                          |                         |the tenant ID of the     |
|                          |                         |client subscribing to    |
|                          |                         |the Cloud Keep service.  |
+--------------------------+-------------------------+-------------------------+
|{project_uuid}            |String                   |This parameter specifies |
|                          |                         |the unique identifier of |
|                          |                         |a project.               |
+--------------------------+-------------------------+-------------------------+


This operation does not accept a request body.


**Example: Get project quota details cURL request**


.. code::

   curl -H 'Accept: application/json' \
        -H 'X-Auth-Token:<token>'\
        $ENDPOINT/project-quotas/{uuid}


Response
""""""""""""""""

The following table shows the response attributes for this request.

+----------------+---------+--------------------------------------------------------------+
| Name           | Type    | Description                                                  |
+================+=========+==============================================================+
| project-quotas | dict    | Contains a dictionary with project quota information.        |
+----------------+---------+--------------------------------------------------------------+
| secrets        | integer | Contains the configured quota value of the requested project |
|                |         | for the secret resource.                                     |
+----------------+---------+--------------------------------------------------------------+
| orders         | integer | Contains the configured quota value of the requested project |
|                |         | for the orders resource.                                     |
+----------------+---------+--------------------------------------------------------------+
| containers     | integer | Contains the configured quota value of the requested project |
|                |         | for the containers resource.                                 |
+----------------+---------+--------------------------------------------------------------+
| consumers      | integer | Contains the configured quota value of the requested project |
|                |         | for the consumers resource.                                  |
+----------------+---------+--------------------------------------------------------------+
| cas            | integer | Contains the configured quota value of the requested project |
|                |         | for the CAs resource.                                        |
+----------------+---------+--------------------------------------------------------------+


**Example: Get project quota details JSON response**


.. code::

        200 OK

        Content-Type: application/json

        {
            "project_quotas": {
            "secrets": 10,
            "orders": 20,
            "containers": -1,
            "consumers": 10,
            "cas": 5
            }
        }
