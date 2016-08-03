
.. _post-secret:

Create Secret
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v1/secrets

This method creates and stores a secret.

..  note::
    The POST request always creates and stores secret metadata. If a payload is provided 
    with the POST request, it is encrypted and stored, and then linked with this metadata. 
    If no payload is provided in the POST request, it must be provided in a subsequent 
    PUT request.


The following table shows possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|201                       |Success                  |This status code is      |
|                          |                         |returned when the secret |
|                          |                         |has been successfully    |
|                          |                         |created.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned if the          |
|                          |                         |"payload" parameter is   |
|                          |                         |empty. This response     |
|                          |                         |indicates that the       |
|                          |                         |'payload' JSON attribute |
|                          |                         |was provided, but no     |
|                          |                         |value was assigned to it.|
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned if the secret   |
|                          |                         |has invalid data. This   |
|                          |                         |response may include     |
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
""""""""""""""""


The following table shows the JSON attributes to be specified in the request:

+--------------------------+------------+--------------------------------------+
|Name                      |Type        |Description                           |
+==========================+============+======================================+
| name                     | string     | Specifies the human                  |
|                          | (optional) | readable name for the                |
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
| expiration               | date       | Specifies the expiration             |
|                          | (optional) | date for the secret in               |
|                          |            | ISO-8601 format. ISO-8601            |
|                          |            | formats dates by using               |
|                          |            | the following                        |
|                          |            | representation:                      |
|                          |            | ``yyyy-mm-ddThh:mm:ss``.             |
|                          |            | For example, September 27,           |
|                          |            | 2012 is represented as               |
|                          |            | ``2012-09-27T00:00:00``. Once the    |
|                          |            | secret has expired, it is            |
|                          |            | no longer returned by the            |
|                          |            | API or agent. This                   |
|                          |            | parameter is optional. If            |
|                          |            | this parameter is not                |
|                          |            | supplied, the secret has             |
|                          |            | no expiration date.                  |
+--------------------------+------------+--------------------------------------+
| payload                  | string     | Specifies the secret's               |
|                          | (optional) | unencrypted plain text (secret data) |
|                          |            | If this parameter is                 |
|                          |            | specified, the                       |
|                          |            | payload_content_type                 |
|                          |            | parameter must be                    |
|                          |            | specified as well. If                |
|                          |            | this parameter is not                |
|                          |            | specified, you can                   |
|                          |            | provide the payload                  |
|                          |            | information via a                    |
|                          |            | subsequent PUT request.              |
|                          |            | If the payload is not                |
|                          |            | provided, only the secret            |
|                          |            | metadata will be                     |
|                          |            | retrievable from Barbican            |
|                          |            | and any attempt to                   |
|                          |            | retrieve decrypted data              |
|                          |            | for that secret will                 |
|                          |            | fail. Deferring the                  |
|                          |            | secret information to a              |
|                          |            | PUT request is useful for            |
|                          |            | secrets that are in                  |
|                          |            | binary format and are not            |
|                          |            | suitable for base64                  |
|                          |            | encoding.                            |
+--------------------------+------------+--------------------------------------+
| payload_content_type     | string     | Specifies the media type (format) of |
|                          | (optional) | the secret data itself.  This        |
|                          |            | parameter is required if             |
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
| payload_content_encoding | string     | Some data might not be suitable to   |
|                          | (optional) | include inside a JSON request.  For  |
|                          |            | example, the contents of a           |
|                          |            | certificate file include newline     |
|                          |            | characters which are not allowed in  |
|                          |            | a JSON request.                      |
|                          |            | To work around this limitation       |
|                          |            | of the JSON format you               |
|                          |            | may optionally base64 encode the     |
|                          |            | secret data since base64 encoding    |
|                          |            | produces a string that contains      |
|                          |            | valid JSON characters.               |
|                          |            | This attribute is used to specify    |
|                          |            | that the data string included in the |
|                          |            | ``payload`` attribute is the bas64   |
|                          |            | encoded representation of the actual |
|                          |            | payload by setting the value to      |
|                          |            | ``base64``.  When set, the Cloud     |
|                          |            | Keep system will base64 decode the   |
|                          |            | string in the payload attribute      |
|                          |            | before encrypting it for storage.    |
|                          |            | When retrieving the secret in future |
|                          |            | requests, the payload will be the    |
|                          |            | decoded data.                        |
+--------------------------+------------+--------------------------------------+


**Example:Create Secret: JSON request**


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
""""""""""""""""

The following table shows the response attribute for this request.

+---------------+---------+-------------------------------------------------------------+
| Name          | Type    | Description                                                 |
+===============+=========+=============================================================+
|secret_ref     | URI     | Returns a HATEOAS url to retrieve information about the     |
|               |         | the specified secret. The reference URL concatenates the    |
|               |         | URI for the 'retrieve secrets` API operation and the        |
|               |         | and the system-generated ``secretID`` assigned automatically|
|               |         | when the secret is created. In the example, the *secretID*  |
|               |         | value is ``485950f0-37a5-4ba4-b1d6-413f79b849ef``.          |
+---------------+---------+-------------------------------------------------------------+

**Example: Create Secret JSON response**


.. code::

   {
       "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/485950f0-37a5-4ba4-b1d6-413f79b849ef"
   }

