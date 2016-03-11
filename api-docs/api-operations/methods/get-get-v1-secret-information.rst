
.. _get-secret-information:

Get secret metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/secrets/{secret_id}

This method retrieves the metadata for the specified secret.

The following table shows possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |Success                  |This status code is      |
|                          |                         |returned when the secret |
|                          |                         |metadata has been        |
|                          |                         |successfully retrieved.  |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |This error code is       |
|                          |                         |returned when the secret |
|                          |                         |id is invalid.           |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""

This operation does not accept a request body.



**Example: Get secret metadata cURL requestt**


.. code::

   curl -H 'Accept: application/json' 
        -H 'X-Auth-Token: $AUTH-TOKEN'\
        $ENDPOINT/v1/secrets/secretID/{secretID}



Response
""""""""""""""""

The following table shows the response parameters for this request.

+---------------+---------+-------------------------------------------------------------+
| Name          | Type    | Description                                                 |
+===============+=========+=============================================================+
|status         | integer | Returns the current state of secret resource.               |
+---------------+---------+-------------------------------------------------------------+
|secret_ref     | URI     | Returns a HATEOAS url to retrieve information about the     |
|               |         | the specified secret.                                       |
+---------------+---------+-------------------------------------------------------------+
|updated        | date    |Returns the date and time that the consumer was last updated.|
+---------------+---------+-------------------------------------------------------------+
|name           | string  |Returns the name assigned to the secret resource when it was |
|               |         |created.                                                     |
+---------------+---------+-------------------------------------------------------------+
|algorithm      | string  |Returns the algorithm type used to generate the secret.      |
+---------------+---------+-------------------------------------------------------------+
|created        | date    |Returns the date and time that the secret was created.       |
+---------------+---------+-------------------------------------------------------------+
|content_types  | dict    |Returns a dictionary of content type information for the     |
|               |         |resource. Supported formats are                              |
|               |         |plain text format (``text/plain``) or binary format          |
|               |         |(``application/octet-stream``). Content types are            |
|               |         |specified when the resource is created.                      |
+---------------+---------+-------------------------------------------------------------+
|mode           | string  |Returns the type/mode of the algorithm associated with the   |
|               |         |secret information. This parameter is optional.              |
+---------------+---------+-------------------------------------------------------------+
|bit_length     | integer |Returns the bit length of the secret resource if available.  |
+---------------+---------+-------------------------------------------------------------+
|expiration     | date    | Returns the expiration date for the secret resource.        |
+---------------+---------+-------------------------------------------------------------+


**Example: Get secret information JSON response**

.. code::

   {
       "status": "ACTIVE",
       "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/485950f0-37a5-4ba4-b1d6-413f79b849ef",
       "updated": "2014-05-02T06:29:25.415271",
       "name": "AES key",
       "algorithm": "aes",
       "created": "2014-05-02T06:29:25.415261",
       "content_types": {
           "default": "application/octet-stream"
       },
       "mode": "cbc",
       "bit_length": 256,
       "expiration": "2014-05-28T19:14:44.180394"
   }

