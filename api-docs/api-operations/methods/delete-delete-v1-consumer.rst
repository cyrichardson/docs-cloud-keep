
.. _delete-consumer:

Delete a consumer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /{version}/{container_ref}/consumers/{consumer_id}


Deletes the specified consumer for the specified container.


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

+----------------------------+---------+---------------------------------+------------+
| Parameter name             | Type    | Description                     | Default    |
+============================+=========+=================================+============+
|containerID                 | string  | The UUID for the container      | None       |
+----------------------------+---------+---------------------------------+------------+
|consumerID                  | string  | The UUID for the consumer       | None       |
+----------------------------+---------+---------------------------------+------------+

The following table shows the body parameters for the request:

+-------------------+---------+--------------------------------------------+------------+
| Parameter name    | Type    | Description                                | Default    |
+===================+=========+============================================+============+
|name               | string  | The name of the consumer set by the user.  | None       |
+-------------------+---------+--------------------------------------------+------------+
|URL                | string  | The url for the user or service using the  | None       |
|                   |         | container.                                 |            |
+-------------------+---------+--------------------------------------------+------------+

**Example: Delete consumer cURL request**

.. code::

   curl -X DELETE -H 'X-Auth-Token: $AUTH-TOKEN' \
        -d '{"name": "consumername", "URL": "consumerURL"}' \
        $ENDPOINT/v1/containers/{containerID}/consumers/{consumerID}

where ``name`` and ``URL`` must match the name and URL that were used when the consumer was created.


Response
""""""""""""""""

The operation returns an HTTP 204 Accepted response code, if successful. 
It does not return a response body.
