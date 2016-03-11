
.. _get-container-information:

Get Container Information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/containers/{container_id}

This method retrieves information about a specified container.


The following table shows the possible response codes for this operation:


+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 200  | Successful Request                                                          |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 404  | Container not found or unavailable                                          |
+------+-----------------------------------------------------------------------------+


Request
""""""""""""""""


The following table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{container_id}            |String *(Required)*      |This parameter specifies |
|                          |                         |the unique identifier of |
|                          |                         |a container that has     |
|                          |                         |been stored.             |
+--------------------------+-------------------------+-------------------------+



This operation does not accept a request body.


**Example: Get Container Information cURL request**


.. code::

      curl -H 'Accept: application/json' -H 'X-Auth-Token:$AUTH-TOKEN' \
         $ENDPOINT/v1/containers/{containerID}



Response
""""""""""""""""

The following table shows the response parameters for this request.

+-----------------+-----------+----------------------------------------------------------+
| Name            | Type      | Description                                              |
+=================+===========+==========================================================+
|**type**         | string    |Indicates the container type: *generic*, *rsa*, or        |
|                 |           |*certificate*.                                            |
+-----------------+-----------+----------------------------------------------------------+
|**status**       | string    |Returns the current state for the specified container.    |
+-----------------+-----------+----------------------------------------------------------+
|**name**         | string    |The name assigned to the specified container when it was  |     
|                 |           |created.                                                  |
+-----------------+-----------+----------------------------------------------------------+
|**consumers**    | dict      |Returns a list of dictionaries with information about the |
|                 |           |consumers included in the specified container.            | 
+-----------------+-----------+----------------------------------------------------------+
|**container_ref**| URI       |A HATEOS url to retrieve information about the specified  |
+-----------------+-----------+----------------------------------------------------------+
|secret_refs      | dict      |Returns a dictionary with information about the secrets   |
|                 |           |included in the container.                                |
+-----------------+-----------+----------------------------------------------------------+
|secret_refs.\    | string    |The name assigned to the secret resource when it was      |
|**name**         |           |created.                                                  |
+-----------------+-----------+----------------------------------------------------------+
|secret_refs.\    | URI       | A HATEOAS url to retrieve information about the specified|
|**secret_ref**   |           | secret.                                                  |
+-----------------+-----------+----------------------------------------------------------+
|**created**      | date      | The date and time that the container was created.        |
+-----------------+-----------+----------------------------------------------------------+
|**updated**      | date      | The date and time that the container was last updated.   |
+-----------------+----------+-----------------------------------------------------------+


**Example: Get container information JSON response**


.. code::

    {
        "type": "generic",
        "status": "ACTIVE",
        "name": "container name",
        "consumers": [],
        "container_ref": "https://iad.keep.api.rackspacecloud.com/v1/containers/6ad67bc0-17fd-45ce-b84a-a9be44fe069b",
        "secret_refs": [
          {
              "name": "private_key",
              "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/485950f0-37a5-4ba4-b1d6-413f79b849ef"
          }
        ],
        "created": "2015-03-26T21:10:45.417835",
        "updated": "2015-03-26T21:10:45.417835"
    }
