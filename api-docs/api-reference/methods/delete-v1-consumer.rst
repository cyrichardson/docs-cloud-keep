
.. _delete-consumer:

Delete a consumer
~~~~~~~~~~~~~~~~~

.. code::

    DELETE /{version}/{container_ref}/consumers/{consumer_id}


This operation deletes the specified consumer for the specified container.

The following table shows the possible response codes for this operation.

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
-------

The following table shows the URI parameters for the request.

+----------------------------+---------+---------------------------------+
| Parameter name             | Type    | Description                     |
+============================+=========+=================================+
|container_id                | string  | The UUID for the container      |
+----------------------------+---------+---------------------------------+
|consumer_id                 | string  | The UUID for the consumer       |
+----------------------------+---------+---------------------------------+

The following table shows the body parameters for the request:

+-------------------+---------+--------------------------------------------+
| Parameter name    | Type    | Description                                |
+===================+=========+============================================+
|name               | string  | The name of the consumer set by the user.  |
|                   |         | The name must match the name that was used |
|                   |         | when the consumer was created.             |
+-------------------+---------+--------------------------------------------+
|URL                | string  | The URL for the user or service using the  |
|                   |         | container. The URL must match the URL that |
|                   |         | was used when the consumer was created.    |
+-------------------+---------+--------------------------------------------+

**Example: Delete a consumer, cURL request**

.. code::

   curl -X DELETE -H 'X-Auth-Token: $AUTH-TOKEN' \
        -d '{"name": "consumername", "URL": "consumerURL"}' \
        $ENDPOINT/v1/containers/{containerID}/consumers/{consumerID}

where ``name`` and ``URL`` must match the name and URL that were used when
the consumer was created.


Response
--------

The operation returns an HTTP 204 Accepted response code, if successful.
It does not return a response body.
