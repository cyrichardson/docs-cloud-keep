
.. _delete-secret:

Delete a secret
~~~~~~~~~~~~~~~

.. code::

    DELETE /v1/secrets/{secret_id}

This operation deletes the specified secret.

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
-------

The following table shows the URI parameter for the request:

+----------------------------+---------+---------------------------------+
| Parameter name             | Type    | Description                     |
+============================+=========+=================================+
| secretID                   | string  | The UUID for the secret         |
+----------------------------+---------+---------------------------------+

This operation does not accept a request body.

**Example: Delete a secret, cURL request**


.. code::

   curl -X DELETE -H "X-Auth-Token: $AUTH_TOKEN" \
        $ENDPOINT/v1/secrets/{secretID}


Response
--------

The operation returns an HTTP 204 Accepted response code, if successful.
It does not return a response body.
