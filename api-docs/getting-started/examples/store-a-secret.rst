
.. _gsg-store-a-secret:

Store a secret
~~~~~~~~~~~~~~~~~~~~


You can store a secret by submitting a **POST** request against the
secrets resource and include the secret in the *``payload``* parameter.
You specify the secret payload type in the ``payload_content_type``
parameter:

-  For text-based secrets, set the ``payload_content_type`` parameter
   to ``text/plain``.

-  For binary secrets, set the ``payload_content_type`` parameter to
   ``application/octet-stream``.

..  note::

      Note
      The secret resource encrypts and stores client-provided secret
      information and metadata.  Submitting a **POST** request creates secret metadata.
      If the payload is provided with the **POST** request, then it is encrypted and stored, and
      then linked with this metadata. If no payload is included with the
      **POST** request, it must be provided with a subsequent **PUT** request.

      The following example shows how to store a secret in the format of an
      AES key by submitting a **POST** request wth the base64-encoded secret
      payload specified against the secrets resource.

.. code::

      $ curl -X POST -H 'Content-Type: application/json' -H 'Accept: application/json'\
      -H 'X-Auth-Token: '$AUTH_TOKEN -d\
        '{
            "name": "AES key",
            "expiration": "2020-02-28T19:14:44.180394",
            "algorithm": "aes",
            "bit_length": 256,
            "mode": "cbc",
            "payload": "gF6+lLoF3ohA9aPRpt+6bQ==",
            "payload_content_type": "application/octet-stream",
            "payload_content_encoding": "base64"
          }' $API_ENDPOINT/v1/secrets


If the request is successful, you will receive a response like the
following:

.. code::

        "{"secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/578391c7-92fa-484f-8546-3562b170e5"}"


The example above shows the secretId (578391c7-92fa-484f-8546-3562b170e5), which will be returned in a
successful response from the endpoint https://iad.keep.api.rackspacecloud.com.

For subsequent API calls requiring a secret ID, you should set an environment variable as follows:

.. code::

      $ export SECRET_ID=578391c7-92fa-484f-8546-3562b170e5

..  note::

      Note
      You can also store a secret by first submitting a **POST** request
      without specifying the secret payload and then submitting a subsequent
      **PUT** request with the payload. This storage mode enables you to
      upload a a binary file to Cloud Keep directly for encrypted
      storage. For more information, read :ref:`gsg-two-step-secret-creation`.
