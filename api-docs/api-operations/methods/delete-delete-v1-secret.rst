
.. _delete-secret:

Delete a secret
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /{version}/secrets/{secret_id}



Deletes the specified secret.

The following table shows the possible response codes for this operation:


+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 204  | Successful request                                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 404  | Secret not found                                                            |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""

The following table shows the URI parameter for the request:

+----------------------------+---------+---------------------------------+------------+
| Parameter name             | Type    | Description                     | Default    |
+============================+=========+=================================+============+
| secretID                   | string  | The UUID for the secret         | None       |
+----------------------------+---------+---------------------------------+------------+

This operation doesn't take a request body.

**Example: Delete secret cURL request**


.. code::

   curl -X DELETE -H 'X-Auth-Token: $AUTH-TOKEN' \
        $ENDPOINT/v1/secrets/{secretID}


Response
""""""""""""""""

The operation returns an HTTP 204 Accepted response code, if successful. 
It does not return a response body.
