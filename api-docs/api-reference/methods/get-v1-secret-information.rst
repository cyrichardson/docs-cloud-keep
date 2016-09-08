
.. _get-secret-information:

Retrieve secret metadata
~~~~~~~~~~~~~~~~~~~~~~~~

.. code::

    GET /v1/secrets/{secret_id}

This operation retrieves the metadata for the specified secret.

The following table shows possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |Success                  |This status code is      |
|                          |                         |returned when the secret |
|                          |                         |metadata has been        |
|                          |                         |successfully retrieved.  |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |This error code is       |
|                          |                         |returned when the secret |
|                          |                         |ID is invalid.           |
+--------------------------+-------------------------+-------------------------+


Request
-------

he following table shows the URI parameters for this request.

+---------------+---------+----------------------------------------------------+
| Name          | Type    | Description                                        |
+===============+=========+====================================================+
| {secretID}    | string  | Human readable name for the secret.                |
+---------------+---------+----------------------------------------------------+

This operation does not accept a request body.

**Example: Retrieve secret metadata, cURL request**

.. code::

   curl -H 'Accept: application/json' \
        -H "X-Auth-Token: $AUTH_TOKEN" \
        $ENDPOINT/v1/secrets/{secretID}

Response
--------

The following table shows the response attributes.

+---------------+---------+---------------------------------------------------------------+
| Name          | Type    | Description                                                   |
+===============+=========+===============================================================+
| name          | string  | Human readable name for the secret assigned when the secret   |
|               |         | was created.                                                  |
+---------------+---------+---------------------------------------------------------------+
| status        | string  | Returns the current state of the secret resource. Possible    |
|               |         | values are ``ACTIVE``, ``PENDING``, ``ERROR``.                |
+---------------+---------+---------------------------------------------------------------+
| secret\_ref   | URI     | A HATEOS URL to retrieve information about the specified      |
|               |         | secret. This value is assigned by the API.                    |
+---------------+---------+---------------------------------------------------------------+
| secret\_type  | string  | The secret type. The possible secret types are:               |
|               |         |                                                               |
|               |         |     - ``symmetric``                                           |
|               |         |     - ``public``                                              |
|               |         |     - ``private``                                             |
|               |         |     - ``passphrase``                                          |
|               |         |     - ``certificate``                                         |
|               |         |     - ``opaque``                                              |
|               |         |                                                               |
+---------------+---------+---------------------------------------------------------------+
| creator_id    | integer | User ID of the user who created the secret.                   |
+---------------+---------+---------------------------------------------------------------+
| created       | date    | UTC time stamp of when the secret was created.                |
+---------------+---------+---------------------------------------------------------------+
| updated       | date    | UTC time stamp of when the secret was last updated.           |
+---------------+---------+---------------------------------------------------------------+
| expiration    | date    | The expiration date for the secret in ISO-8601 format. Once   |
|               |         | the secret has expired, it will no longer be returned by the  |
|               |         | API.                                                          |
+---------------+---------+---------------------------------------------------------------+
| content_types | dict    | Dictionary of content type information for the resource.      |
|               |         | Supported formats are plain text format (text/plain) and      |
|               |         | binary format (application/octet-stream). Content types are   |
|               |         | specified when the resource is created.                       |
+---------------+---------+---------------------------------------------------------------+
| algorithm     | string  | (Deprecated) Metadata describing the algorithm associated     |
|               |         | with the secret.                                              |
+---------------+---------+---------------------------------------------------------------+
| mode          | string  | (Deprecated) Metadata describing the mode of the algorithm    |
|               |         | associated with the secret.                                   |
+---------------+---------+---------------------------------------------------------------+
| bit_length    | string  | (Deprecated) Metadata describing the bit length of the secret.|
+---------------+---------+---------------------------------------------------------------+



**Example: Retrieve secret metadata, JSON response**

.. code::

    {
        "status": "ACTIVE",
        "secret_type": "private",
        "updated": "2016-07-13T15:27:04",
        "name": "My RSA private key",
        "algorithm": null,
        "created": "2016-07-12T23:20:42",
        "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/93d9052f-c4d0-4e39-8d4a-d997db2819f9",
        "content_types": {
            "default": "application/octet-stream"
        },
        "creator_id": "123456",
        "mode": null,
        "bit_length": null,
        "expiration": null
    }
