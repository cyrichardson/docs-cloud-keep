
.. _post-consumers:

Create a consumer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /{version}/containers/{container_id}/consumers


Creates a consumer for the specified container.

The following table shows the possible response codes for this operation:

+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 201  | Successful creation of the consumer                                         |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 403  | Forbidden.  The user has been authenticated, but is not authorized to       |
|      | create a consumer.  This can be based on the the user's role or the         |
|      | project's quota.                                                            |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""


There are no URL parameters for this request.


The following table shows the body parameters for the request:

+-------------------+---------+--------------------------------------------+------------+
| Parameter name    | Type    | Description                                | Default    |
+===================+=========+============================================+============+
|name               | string  | The name of the consumer set by the user.  | None       |
+-------------------+---------+--------------------------------------------+------------+
|URL                | string  | The url for the user or service using the  | None       |
|                   |         | container.                                 |            |
+-------------------+---------+--------------------------------------------+------------+
|containerID        | string  | The UUID for the container                 | None       |
+-------------------+---------+--------------------------------------------+------------+


**Example: Create consumer cURL request**


.. code::

      curl -X POST -H 'X-Auth-Token $AUTH-TOKEN' \
           -H 'Content-Type: application/json' \
           -d '{
                 "name": "your consumer name",
                  "URL": "{consumerURL}"
              }' \
           $ENDPOINT/v1/containers/{containerID}/consumers
           

Response
""""""""""""""""



**Example: Create Consumer JSON response**


.. code::

    {
        "status": "ACTIVE",
        "updated": "2015-10-15T17:56:18.626724",
        "name": "your container name",
        "consumers": [
            {
                "URL": "https://consum.er",
                "name": "your consumer name"
            }
    }

where:

- the consumer URL is https://consum.er
