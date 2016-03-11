
.. _get-project-quota-details:

Get Project quota details
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/project-quotas/{project_id}

The get project quota details operation, retrieves the project quota information 
configured for the specified project.  This is different
from the get quotas operation which returns the resolved quotas. 

This call returns only the values set for quotas at the project level.  Quotas are resolved 
by taking the system level of quotas and overriding any project-level quotas.

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
|{project_id}              |String                   |This parameter specifies |
|                          |                         |the unique identifier of |
|                          |                         |a project.               |
+--------------------------+-------------------------+-------------------------+


This operation does not accept a request body.


**Example: Get project quota details cURL request**


.. code::

   curl -H 'Accept: application/json' -H 'X-Auth-Token:$AUTH_TOKEN'\
        $ENDPOINT/v1/project-quotas/{projectID}


Response
""""""""""""""""

The following table shows the response attributes for this request.

+-------------------+---------+----------------------------------------------------------+
| Name              | Type    | Description                                              |
+===================+=========+==========================================================+
|**project-quotas** | dict    | Contains a dictionary with project quota information.    |
+-------------------+---------+----------------------------------------------------------+
|project-quotas.\| integer | Contains the configured quota value of the requested project|
|**secrets**     |         | for the secrets resource.                                   |
+----------------+---------+-------------------------------------------------------------+
|project-quotas.\| integer | Reserved for future use.                                    |
|**orders**      |         |                                                             |
+----------------+---------+-------------------------------------------------------------+
|project-quotas.\| integer | Contains the configured quota value of the requested project|
|**containers**  |         | for the containers resource.                                |
+----------------+---------+-------------------------------------------------------------+
|project-quotas.\| integer | Contains the configured quota value of the requested project|
|**consumers**   |         | for the consumers resource.                                 |
+----------------+---------+-------------------------------------------------------------+
|project-quotas.\| integer |  Reserved for future use.                                   |
|**cas**         |         |                                                             |
+----------------+---------+-------------------------------------------------------------+


**Example: Get project quota details JSON response**


.. code::

        {
            "project_quotas": {
                "secrets": 10,
                "orders": 0,
                "containers": -1,
                "consumers": 10,
                "cas": 0
                }
        }
