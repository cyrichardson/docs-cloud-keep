
.. _delete-project-quota-configuration:

Delete the project quotas configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /v1/project-quotas/{uuid}

Delete the project quotas configuration for the project with the requested UUID. After 
the project quota configuration is deleted, the default quotas are used for 
the specified project.

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

The following table shows the URI parameter for the request:

+----------------------------+---------+---------------------------------+------------+
| Parameter name             | Type    | Description                     | Default    |
+============================+=========+=================================+============+
| uuid                       | string  | The UUID for the container      | None       |
+----------------------------+---------+---------------------------------+------------+


This operation does not accept a request body.


**Example: Delete container cURL request**


.. code::

   curl -X DELETE -H 'X-Auth-Token: $AUTH-TOKEN' \
        $ENDPOINT/v1/project-quotas/{uuid}


Response
""""""""""""""""

The operation returns an HTTP 204 Accepted response code, if successful. 
It does not return a response body.
