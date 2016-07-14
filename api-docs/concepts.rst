.. _concepts:

Concepts
----------

Review the following key concepts and architectural overview to learn how |product name|
enables secure life-cycle management for keys and credentials.


.. _secrets-concept:

Secrets
~~~~~~~~~~~~~~~~~~

A secret is a singular item that is stored within |product name|. It is
any data that requires security conscious storage such as a key,
credential, configuration file, etc.  The typical use case for a secret
is an encryption key that you wish to store away from prying eyes.

Some examples of a secret may include:
  * Private RSA Key
  * X.509 Certificate
  * Passphrase
  * SSH Key

The secret schema represents the actual secret or key that is presented
to the |product name| service.  Secrets themselves can be any format.

The following example shows the specification for a secret passphrase that
has been added to |product name|:

.. code::

    {
        "status": "ACTIVE",
        "secret_type": "passphrase",
        "updated": "2016-07-08T21:51:19",
        "name": "Database administrator passphrase",
        "algorithm": null,
        "created": "2016-07-08T21:51:19",
        "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/0f1afafb-36f7-4976-a3bc-2cc3b4af4059",
        "content_types": {
            "default": "text/plain"
        },
        "creator_id": "123456",
        "mode": null,
        "bit_length": null,
        "expiration": "2020-01-31T00:00:00"
    }

A secret consists of the following elements:

+---------------+---------------------------------------------------------------+
| Element       | Description                                                   |
+===============+===============================================================+
| name          | Human readable name for the secret.                           |
+---------------+---------------------------------------------------------------+
| status        | The secret's status.  Possible values are ``ACTIVE``,         |
|               | ``PENDING``, ``ERROR``.                                       |
+---------------+---------------------------------------------------------------+
| secret\_ref   | Unique identifier for the secret. This value is assigned by   |
|               | the API.                                                      |
+---------------+---------------------------------------------------------------+
| secret\_type  | The secret type. The possible secret types are:               |
|               |                                                               |
|               |     - ``symmetric``: Used for storing byte arrays such as     |
|               |       keys suitable for symmetric encryption.                 |
|               |     - ``public``: Used for storing the public key of an       |
|               |       asymmetric keypair.                                     |
|               |     - ``private``: Used for storing the private key of an     |
|               |       asymmetric keypair.                                     |
|               |     - ``passphrase``: Used for storing plain text             |
|               |       passphrases.                                            |
|               |     - ``certificate``: Used for storing cryptographic         |
|               |       certificates such as X.509 certificates.                |
|               |     - ``opaque`` (default): Used for storing unformatted data |
|               |                                                               |
+---------------+---------------------------------------------------------------+
| creator_id    | User ID of the user who created the secret.                   |
+---------------+---------------------------------------------------------------+
| created       | UTC time stamp of when the secret was created.                |
+---------------+---------------------------------------------------------------+
| updated       | UTC time stamp of when the secret was last updated.           |
+---------------+---------------------------------------------------------------+
| expiration    | The expiration date for the secret in ISO-8601 format. Once   |
|               | the secret has expired, it will no longer be returned by the  |
|               | API.                                                          |
+---------------+---------------------------------------------------------------+
| content_types | Media Type(s) associated with this secret.                    |
+---------------+---------------------------------------------------------------+
| algorithm     | (Deprecated) Metadata describing the algorithm associated     |
|               | with the secret.                                              |
+---------------+---------------------------------------------------------------+
| mode          | (Deprecated) Metadata describing the mode of the algorithm    |
|               | associated with the secret.                                   |
+---------------+---------------------------------------------------------------+
| bit_length    | (Deprecated) Metadata describing the bit length of the secret.|
+---------------+---------------------------------------------------------------+


You can use one of the following methods to store a secret:

-  Submit a **POST** request against the secrets resource. Include both
   the secret metadata and the secret data itself (the payload as it is called
   in Cloud Keep) in the JSON body.

-  Submit a **POST** request without a ``payload`` attribute against the
   secrets resource and then include the payload in a subsequent **PUT**
   request against the secret that was created by the POST. This mode enables
   you to upload payloads that cannot be included inside the JSON body, such
   as a binary file, to the |product name| system directly for encrypted storage.

..  note::
        Note
        Submitting a **POST** request creates secret metadata. If the payload is
        provided inside the JSON body of the  **POST** request, then it is
        encrypted and stored, and then linked with this metadata. If no payload
        is included within the **POST** request, then it must be provided with
        a subsequent **PUT** request.  The secret resource encrypts and stores
        both, the client-provided secret data (payload) and metadata.


.. _containers-concept:

Container
~~~~~~~~~~~~~~~~~~

The containers resource is the organizational center piece of |product name|.
It can simplify secret management in environments that have large numbers of
secrets.

A container is a logical object that can be used to store secret references that are related by relationship or type.
For example you can create a single container to group a private key, certificate, and intermediate certificates bundle for
a TLS certificate. Containers simplify the task of managing large numbers of secrets resources.

|product name| supports 3 types of containers:
  * :ref:`Generic <generic_containers>`
  * :ref:`Certificate <certificate_containers>`
  * :ref:`RSA <rsa_containers>`

Each of these types have explicit restrictions as to what type of secrets should be
held within. These will be broken down in their respective sections.


.. _generic_containers:

Generic Containers
^^^^^^^^^^^^^^^^^^^^^

A generic container is used for any type of container that a user may wish to create.
There are no restrictions on the type or amount of secrets that can be held within a container.

An example of a use case for a generic container would be having multiple passwords stored
in the same container reference:

.. code-block:: json

    {
        "status": "ACTIVE",
        "updated": "2016-07-12T21:35:24",
        "name": "My generic container",
        "consumers": [],
        "created": "2016-07-12T21:35:24",
        "container_ref": "https://iad.keep.api.rackspacecloud.com/v1/containers/c2c09737-1eb7-428c-be6e-d2b4f2ded016",
        "creator_id": "123456",
        "secret_refs": [
            {
                "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/b01f4952-68b2-4baa-a62c-f342b55a044f",
                "name": "Another Secret"
            },
            {
                "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/b5a6496a-633c-4048-a065-50042787835b",
                "name": "One secret"
            }
        ],
        "type": "generic"
    }

.. _certificate_containers:

Certificate Containers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A certificate container is used to group X.509 Certificates with other secrets
that are needed to successfully use the certificate.  For example:

  * certificate
  * private_key (optional)
  * private_key_passphrase (optional)
  * intermediate certificate chain (optional)

.. code-block:: json

    {
        "status": "ACTIVE",
        "updated": "2016-07-13T16:12:56",
        "name": "www.example.com - certificate bundle",
        "consumers": [],
        "created": "2016-07-13T16:12:56",
        "container_ref": "https://iad.keep.api.rackspacecloud.com/v1/containers/1693ecc5-330d-4774-b9e5-ef991cf174d7",
        "creator_id": "344029",
        "secret_refs": [
            {
                "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/ce3a6b55-4951-469d-93b1-b20d46500b80",
                "name": "intermediates"
            },
            {
                "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/93d9052f-c4d0-4e39-8d4a-d997db2819f9",
                "name": "private_key"
            },
            {
                "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/c506c2cf-b2a0-4ac4-b862-59fe6a0dedbc",
                "name": "certificate"
            }
        ],
        "type": "certificate"
    }

The payload for the secret referenced as the "certificate" is expected to be a
PEM formatted X.509 certificate.

The payload for the secret referenced as the "intermediates" is expected to be a
PEM formatted PKCS#7 certificate chain.

The payload for the secret referenced as the "private_key" is expected to be a
PKCS#8 RSA private key.


.. _rsa_containers:

RSA Containers
^^^^^^^^^^^^^^^^^^

An RSA container is used for grouping RSA private keys with their public keys,
and optionally a private key passphrase for RSA keys that are passphrase-protected.

.. code-block:: json

    {
        "status": "ACTIVE",
        "updated": "2016-07-13T18:09:03",
        "name": "My RSA keypair",
        "consumers": [],
        "created": "2016-07-13T18:09:03",
        "container_ref": "https://iad.keep.api.rackspacecloud.com/v1/containers/01b0c408-910c-4648-8c22-5c9da4bf1b01",
        "creator_id": "123456",
        "secret_refs": [
            {
                "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/23589c54-2dea-4ab6-8395-cc289d137738",
                "name": "public_key"
            },
            {
                "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/93d9052f-c4d0-4e39-8d4a-d997db2819f9",
                "name": "private_key"
            }
        ],
        "type": "rsa"
    }

.. _quotas-concept:

Quotas
~~~~~~~~~~~~~~~~~~

All users authenticated with |product name| can read the effective quota values
that apply to their account. |product name| identifies the account for a user based on
the data included in the authentication token.

Quotas are enforced for the following |product name| resources: secrets, containers,
and consumers.  The following table describes the possible values for the quota attribute.

.. csv-table::
   :header: "Value", "Description"
   :widths: 15, 40

   "Any positive integer", "Defines the maximum number of resources allowed for your account"
   "0", "Indicates that a resource has been effectively disabled"
   "-1", "Indicates that the account has no limits on the number of resources you can
   create."

Please contact your account representative if you would like to raise the quota
limits on your account.

.. _consumer_concept:


Consumer
~~~~~~~~~~~~~~~~~~

A consumer provides a method to register as an interested party for a container.
For example, when a Load Balancer is using a certificate bundle stored in |product name|
it will register itself as a consumer of the certificate container.

You can get a list of consumers for a container by submitting a
:ref:`retrieve consumers <get-containers-consumers>` API request

To prevent unexpected service problems, ensure that you notify all
consumers before you delete a container.
