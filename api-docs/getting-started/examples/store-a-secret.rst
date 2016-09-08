
.. _gsg-store-a-secret:

Store a secret
~~~~~~~~~~~~~~

You can store a secret by submitting a **POST** request against the
secrets resource and including the secret data in the ``payload`` attribute in
the json body of the request.
You must also specify the media type of secret payload in the
``payload_content_type`` attribute of the json body:

-  For ``passphrase`` type secrets, set the ``payload_content_type`` parameter
   to ``text/plain``.

-  For binary secrets such as ``symmetric`` type secrets, set the
   ``payload_content_type`` attribute to ``application/octet-stream``.

-  For ``certificate`` type secrets, set the ``payload_content_type``
   attribute to ``application/pkix-cert``.

..  note::

      The secrets resource stores both the metadata describing the secret as
      well as the encrypted secret data.
      Submitting a **POST** request creates secret metadata.  If the payload
      is provided in the json body of the **POST** request, it is
      encrypted and stored, and linked with this metadata. If no payload is
      included with the  **POST** request, it must be provided in a
      subsequent **PUT** request.

The following example shows how to store a secret in the format of a
passphrase by submitting a **POST** request that includes the payload
in the json body.

**Example: Store a secret, request**

.. code::

   $ curl -X POST -H "Content-Type: application/json"
          -H "Accept: application/json" \
          -H "X-Auth-Token: $AUTH_TOKEN" -d \
             {
                 "name": "A secret passphrase",
                 "secret_type": "passphrase",
                 "expiration": "2020-02-28T23:59:59",
                 "payload": "1 very hard to guess pa$$phrase",
                 "payload_content_type": "text/plain"
             }' $ENDPOINT/v1/secrets


If the request is successful, you will receive a response like the
following one:

**Example: Store a secret, response**

.. code::

   {"secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/578391c7-92fa-484f-8546-3562b170e5"}


The preceding example shows the secret Id (578391c7-92fa-484f-8546-3562b170e5),
which will be returned in a successful response from the
``https://iad.keep.api.rackspacecloud.com`` endpoint.

For subsequent API calls that require a secret ID, you should set an environment
variable as follows:

.. code::

      $ export SECRET_ID=578391c7-92fa-484f-8546-3562b170e5

..  note::

      Note
      You can also store a secret by first submitting a **POST** request
      without specifying the secret payload and then submitting a subsequent
      **PUT** request with the payload. This storage mode enables you to
      upload a a binary file to Cloud Keep directly for encrypted
      storage. For more information, see :ref:`gsg-two-step-secret-creation`.
