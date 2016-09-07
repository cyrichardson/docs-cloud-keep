.. _gsg-retrieve-list-of-stored-secrets:

Retrieve a list of stored secrets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Perform a **GET** request on the secrets resource to retrieve a list of
:ref:`secrets <secrets-concept>` that belong to your tenant.

By default, the API request returns the first 10 secrets associated with the
tenant. You
can use the *limit* and *offset* request parameters to limit the maximum
number of secrets returned in a single request and to set the starting point
for the list.

The following example specifies ``limit`` and ``offset`` values to return five
secrets, starting with the first.


**Example: Retrieve list of secrets request**

.. code::

    $ curl -X GET $ENDPOINT/v1/secrets?limit=5\&offset=0 \
         -H "Accept: application/json" \
         -H "X-Auth-Token: $AUTH_TOKEN" \
         -H "Content-Type: application/json" \
         | python -m json.tool



If the operation is successful, the response returns a list of secrets as
shown in the following example.

.. note::

    If additional secrets have been stored, the returned data contains
    ``next`` and ``previous`` links so that you can page through the data.



**Example:  Retrieve list of secrets response**

.. code::

    {
        "secrets": [
            {
                "status": "ACTIVE",
                "secret_type": "opaque",
                "updated": "2016-06-09T15:48:10",
                "name": "transport secret",
                "algorithm": null,
                "created": "2016-06-09T15:48:10",
                "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/e88e0cfc-8c64-4b72-8e01-5988f704659a",
                "creator_id": "123456",
                "mode": null,
                "bit_length": null,
                "expiration": null
            },
            {
                "status": "ACTIVE",
                "secret_type": "passphrase",
                "updated": "2016-07-11T19:28:38",
                "name": "A secret passphrase",
                "algorithm": null,
                "created": "2016-07-11T19:28:38",
                "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/6467b483-5233-4409-a99d-4db5cf86fe6d",
                "content_types": {
                    "default": "text/plain"
                },
                "creator_id": "123456",
                "mode": null,
                "bit_length": null,
                "expiration": "2020-02-28T23:59:59"
            },
            {
                "status": "ACTIVE",
                "secret_type": "passphrase",
                "updated": "2016-07-11T20:59:58",
                "name": "A secret passphrase",
                "algorithm": null,
                "created": "2016-07-11T20:59:58",
                "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/6538b657-8402-4920-abed-25e7ca5e5adf",
                "content_types": {
                    "default": "text/plain"
                },
                "creator_id": "123456",
                "mode": null,
                "bit_length": null,
                "expiration": "2020-02-28T23:59:59"
            },
            {
                "status": "ACTIVE",
                "secret_type": "passphrase",
                "updated": "2016-07-08T21:51:19",
                "name": "Database administrator passphrase",
                "algorithm": null,
                "created": "2016-07-08T21:51:19",
                "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/ca5bd87f-421a-4ed2-9a22-1874f2a808c0",
                "content_types": {
                    "default": "text/plain"
                },
                "creator_id": "123456",
                "mode": null,
                "bit_length": null,
                "expiration": "2020-01-31T00:00:00"
            },
            {
                "status": "ACTIVE",
                "secret_type": "private",
                "updated": "2016-05-31T17:33:08",
                "name": null,
                "algorithm": "rsa",
                "created": "2016-05-31T17:33:08",
                "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/948b98df-a774-4827-9a73-eac45568c91a",
                "content_types": {
                    "default": "text/plain"
                },
                "creator_id": "123456",
                "mode": "cbc",
                "bit_length": 256,
                "expiration": null
            }
        ],
        "total": 7,
        "next": "https://iad.keep.api.rackspacecloud.com/v1/secrets?limit=5&offset=5"
    }
