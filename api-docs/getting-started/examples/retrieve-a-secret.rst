.. _gsg-retrieve-a-secret:

Retrieve a secret
~~~~~~~~~~~~~~~~~

After you have created and stored a secret, you can submit a **GET**
request to retrieve either the secret metadata or the actual decrypted
secret, depending on the URL that is used in the
**GET** request.

- To retrieve only the secret metadata, submit the request to the
  ``/v1/secrets/$SECRET_ID`` resource.
- To retrieve the decrypted secret, submit the request to the
  ``/v1/secrets/$SECRET_ID/payload`` resource.

**Example: Retrieve secret metadata request**

The following example retrieves the secret metadata by
submitting a **GET** request against the endpoint URL with the secret
ID specified.

.. code::

      $ curl -X GET $ENDPOINT/v1/secrets/$SECRET_ID  \
           -H "X-Auth-Token: $AUTH_TOKEN" | python -m json.tool


If the call is successful, the response looks like the following example,
assuming that your ENDPOINT is ``https://iad.keep.api.rackspacecloud.com``:

.. code::

    {
        "status": "ACTIVE",
        "secret_type": "passphrase",
        "updated": "2016-07-11T19:28:38",
        "name": "A secret passphrase",
        "algorithm": null,
        "created": "2016-07-11T19:28:38",
        "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/578391c7-92fa-484f-8546-3562b170e5",
        "content_types": {
            "default": "text/plain"
        },
        "creator_id": "344029",
        "mode": null,
        "bit_length": null,
        "expiration": "2020-02-28T23:59:59"
    }

**Example: Retrieve decrypted secret request**

The following example shows how to retrieve the secret payload by
submitting a **GET** request against the endpoint URL with the secret ID
specified.

.. code::

      $ curl -X GET $ENDPOINT/v1/secrets/$SECRET_ID/payload \
           -H "X-Auth-Token: $AUTH_TOKEN"

If the call is successful, you receive a response containing the decrypted
secret.

.. code::

    1 very hard to guess pa$$phrase
