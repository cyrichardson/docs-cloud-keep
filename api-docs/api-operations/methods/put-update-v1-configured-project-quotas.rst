
.. _put-configured-project-quotas:

Update configured project quotas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    PUT /{version}/project-quotas/{project_id}


Create or update the configured project quotas for the project with the specified project ID.



The following table shows the possible response codes for this operation:


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


The following table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{project_id}              |String *(Required)*      |This parameter specifies |
|                          |                         |the ID for the           |
|                          |                         |specified project.       |
+--------------------------+-------------------------+-------------------------+

The following table shows the body parameters for the request:

+----------------+---------+----------------------------------------------+
| Attribute Name | Type    | Description                                  |
+================+=========+==============================================+
| project-quotas | dict    | A dictionary with project quota information. |
+----------------+---------+----------------------------------------------+
| secrets        | integer | The value to set for this project's secret   |
|                |         | quota.                                       |
+----------------+---------+----------------------------------------------+
| orders         | integer | Reserved for future use.                     |
+----------------+---------+----------------------------------------------+
| containers     | integer | The value to set for this project's          |
|                |         | container quota.                             |
+----------------+---------+----------------------------------------------+
| consumers      | integer | The value to set for this project's          |
|                |         | consumer quota.                              |
+----------------+---------+----------------------------------------------+
| cas            | integer | Reserved for future use.                     |
+----------------+---------+----------------------------------------------+

You only need to specify the values that you want to override.  For example, if
you are only interested in changing the ``secrets`` quota then your project-quotas
dict should only contain an entry for ``secrets``:

.. code::

    {
        "project_quotas": {
                "secrets": 200,
            }
    }

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

**Example: Update project quotas cURL request**


.. code::

      curl -s $ENDPOINT/v1/project-quotas/{projectID} \
           -X PUT \
           -d '{
                 "project_quotas": {
                     "secrets": 50,
                     "orders": 10,
                     "containers": 20
                 }
               }
               ' \
          -H 'X-Auth-Token: $AUTH_TOKEN' \
          -H 'Content-Type: application/json'


Response
""""""""""""""""

The operation returns an HTTP 204 Accepted response code, if successful. 
It does not return a response body.
