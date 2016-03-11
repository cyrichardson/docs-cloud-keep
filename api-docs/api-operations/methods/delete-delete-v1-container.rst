
.. _delete-container:

Delete a container
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /{version}/containers/{container_id}

Deletes a container.

The following table shows the possible response codes for this operation:

+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 204  | Successful deletion of a container                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 404  | Container not found or unavailable                                          |
+------+-----------------------------------------------------------------------------+



Request
""""""""""""""""

The following table shows the URI parameters for the request:

+----------------------------+---------+---------------------------------+------------+
| Parameter name             | Type    | Description                     | Default    |
+============================+=========+=================================+============+
|containerID                 | string  | The UUID for the container      | None       |
+----------------------------+---------+---------------------------------+------------+

This operation does not require a response body.


**Example: Delete container cURL request**


.. code::

   curl -X DELETE -H 'X-Auth-Token: $AUTH-TOKEN' \
        $ENDPOINT/v1/containers/{containerID}


Response
""""""""""""""""

The operation returns an HTTP 204 Accepted response code, if successful. 
It does not return a response body.
