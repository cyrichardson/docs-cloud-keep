
.. _post-secret:

Create a secret
~~~~~~~~~~~~~~~

.. code::

    POST /v1/secrets

This operation creates and stores a secret.

..  note::
    The **POST** request always creates and stores secret metadata. If a
    payload is provided with the **POST** request, it is encrypted and stored,
    and then linked with this metadata. If no payload is provided  the POST request,
    it must be provided in a subsequent **PUT** request.


The following table shows possible response codes for this operation.

+--------------------------+-------------------------+-------------------------+
|Response code             |Name                     |Description              |
+==========================+=========================+=========================+
|201                       |Success                  |This status code is      |
|                          |                         |returned when the secret |
|                          |                         |has been successfully    |
|                          |                         |created.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned if the          |
|                          |                         |``payload`` parameter is |
|                          |                         |empty. This response     |
|                          |                         |indicates that the       |
|                          |                         |'payload' JSON attribute |
|                          |                         |was provided, but no     |
|                          |                         |value was assigned to it.|
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned if the secret   |
|                          |                         |has invalid data. This   |
|                          |                         |response might include   |
|                          |                         |schema violations such   |
|                          |                         |as mime-type not         |
|                          |                         |specified.               |
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned if the value    |
|                          |                         |specified in the         |
|                          |                         |"payload_content_type"   |
|                          |                         |parameter is not         |
|                          |                         |supported. It is caused  |
|                          |                         |when no crypto plugin    |
|                          |                         |supports the             |
|                          |                         |payload_content_type     |
|                          |                         |requested                |
+--------------------------+-------------------------+-------------------------+
|413                       |Error                    |This error code is       |
|                          |                         |returned when the secret |
|                          |                         |specified in the         |
|                          |                         |"payload" parameter is   |
|                          |                         |too large.               |
+--------------------------+-------------------------+-------------------------+


Request
-------


The following table shows the body parameters for the request.

+--------------------------+------------+--------------------------------------+
|Name                      |Type        |Description                           |
+==========================+============+======================================+
| name                     | string     | (Optional) Specifies the human       |
|                          |            | readable name for the                |
|                          |            | secret. This parameter is            |
|                          |            | optional.                            |
+--------------------------+------------+--------------------------------------+
| secret_type              | string     | Specifies the type of                |
|                          |            | secret being stored.                 |
|                          |            | Possible secret types                |
|                          |            | are:                                 |
|                          |            |                                      |
|                          |            |     - ``symmetric``: Used for        |
|                          |            |       storing byte arrays such as    |
|                          |            |       keys suitable for symmetric    |
|                          |            |       encryption.                    |
|                          |            |     - ``public``: Used for storing   |
|                          |            |       the public key of an           |
|                          |            |       asymmetric keypair.            |
|                          |            |     - ``private``: Used for storing  |
|                          |            |       the private key of an          |
|                          |            |       asymmetric keypair.            |
|                          |            |     - ``passphrase``: Used for       |
|                          |            |       storing plain text             |
|                          |            |       passphrases.                   |
|                          |            |     - ``certificate``: Used for      |
|                          |            |       storing cryptographic          |
|                          |            |       certificates such as X.509     |
|                          |            |       certificates.                  |
|                          |            |     - ``opaque`` (default): Used for |
|                          |            |       storing unformatted binary     |
|                          |            |       data                           |
+--------------------------+------------+--------------------------------------+
| expiration               | date       | *(Optional)* Specifies the           |
|                          |            | expiration date for the secret in    |
|                          |            | ISO-8601 format. ISO-8601            |
|                          |            | formats dates by using               |
|                          |            | the following                        |
|                          |            | representation:                      |
|                          |            | ``yyyy-mm-ddThh:mm:ss``.             |
|                          |            | For example, September 27,           |
|                          |            | 2016 is represented as               |
|                          |            | ``2016-09-27T00:00:00``. After the   |
|                          |            | secret has expired, it is            |
|                          |            | no longer returned by the            |
|                          |            | API or agent. This                   |
|                          |            | parameter is optional. If            |
|                          |            | this parameter is not                |
|                          |            | supplied, the secret has             |
|                          |            | no expiration date.                  |
+--------------------------+------------+--------------------------------------+
| payload                  | string     | *(Optional)* Specifies the secret's  |
|                          |            | unencrypted plain text (secret data) |
|                          |            | If this parameter is specified, the  |
|                          |            | ``payload_content_type`` parameter   |
|                          |            | must also be specified.              |
|                          |            | If this parameter is not specified   |
|                          |            | you can provide the payload          |
|                          |            | information via a subsequent **PUT** |
|                          |            | request.                             |
|                          |            |                                      |
|                          |            | If the payload is not provided, only |
|                          |            | metadata will be retrievable from    |
|                          |            | |product name| and any attempt to    |
|                          |            | retrieve decrypted data for that     |
|                          |            | secret will fail. Deferring the      |
|                          |            | secret information to a **PUT**      |
|                          |            | PUT request is useful for  secrets   |
|                          |            | secrets that are in binary format    |
|                          |            | and are not suitable for base 64     |
|                          |            | encoding.                            |
+--------------------------+------------+--------------------------------------+
| payload_content_type     | string     | *(Optional)* Specifies the media type|
|                          |            | format of the secret data itself.    |
|                          |            | This parameter is required if        |
|                          |            | the payload parameter is             |
|                          |            | specified. The following             |
|                          |            | values are supported:                |
|                          |            |                                      |
|                          |            | - ``text/plain`` - This value is     |
|                          |            |   used for *passphrase* type secrets |
|                          |            | - ``application/octet-stream`` -     |
|                          |            |   This value is used for binary data |
|                          |            |   such as *symmetric* and *opaque*   |
|                          |            |   type secrets.                      |
|                          |            | - ``application/pkix-cert`` - This   |
|                          |            |   value is used for "certificate"    |
|                          |            |   type secrets.                      |
+--------------------------+------------+--------------------------------------+
| payload_content_encoding | string     | *(Optional)* Some data might not be  |
|                          | (optional) | suitable to include inside a JSON    |
|                          |            | request. For example, the contents of|
|                          |            | of a certificate file include newline|
|                          |            | characters which are not allowed in  |
|                          |            | a JSON request.                      |
|                          |            |                                      |
|                          |            | To work around this limitation       |
|                          |            | of the JSON format you               |
|                          |            | can optionally base64 encode the     |
|                          |            | secret data because base64 encoding  |
|                          |            | produces a string that contains      |
|                          |            | valid JSON characters.               |
|                          |            |                                      |
|                          |            | Specifies the encoding format used   |
|                          |            | to provide the ``payload`` data.     |
|                          |            | Cloud Keep might translate and store |
|                          |            | the secret data in another format.   |
|                          |            | This parameter is required if the    |
|                          |            | ``payload_content_type`` parameter   |
|                          |            | is set to ``application/octet-       |
|                          |            | ``application/octet-stream``. The    |
|                          |            | only supported value for this        |
|                          |            | paraemeter is ``base64``, which      |
|                          |            | specifies base64- encoded payloads.  |
+--------------------------+------------+--------------------------------------+


**Example: Create a secret, cURL request**


.. code::

   curl -X POST -H 'Content-Type: application/json' \
        -H 'Accept: application/json' -H "X-Auth-Token: $AUTH_TOKEN" -d \
        '{
            "name": "Rocket launch codes",
            "secret_type": "passphrase",
            "payload": "secretsecretsecret",
            "payload_content_type": "text/plain",
            "expiration": "2020-01-31T23:59:59"
         }' $ENDPOINT/v1/secrets


Response
--------

The following table shows the response attribute.

+---------------+---------+-------------------------------------------------------------+
| Name          | Type    | Description                                                 |
+===============+=========+=============================================================+
|secret_ref     | URI     | Returns a HATEOAS URL to retrieve information about the     |
|               |         | the specified secret. The reference URL concatenates the    |
|               |         | URI for the retrieve secrets API operation and the          |
|               |         | and the system-generated secret ID assigned automatically   |
|               |         | when the secret is created. In this example, the secret ID  |
|               |         | value is ``485950f0-37a5-4ba4-b1d6-413f79b849ef``.          |
+---------------+---------+-------------------------------------------------------------+

**Example: Create a secret, JSON response**


.. code::

   {
       "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/485950f0-37a5-4ba4-b1d6-413f79b849ef"
   }
