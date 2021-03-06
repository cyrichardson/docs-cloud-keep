.. _concepts:

==================
|service| concepts
==================

Review the following key concepts and architectural overview to learn how
|product name| enables secure life-cycle management for keys and credentials.


.. _secrets-concept:

Secrets
~~~~~~~

A *secret* is a single item that is stored within |product name|. A secret is
any data that requires security conscious storage such as a key,
credential, configuration file, etc.  The typical use case for a secret
is an encryption key that you want to keep safe.

Following are some examples of a secret:

  * Private RSA Key
  * X.509 Certificate
  * Passphrase
  * SSH Key

The secret schema represents the actual data that is presented
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

A secret has the following attributes:

+---------------+---------------------------------------------------------------+
| Attribute     | Description                                                   |
+===============+===============================================================+
| name          | Human readable name for the secret.                           |
+---------------+---------------------------------------------------------------+
| status        | The secret's status.  Possible values are ``ACTIVE``,         |
|               | ``PENDING``, ``ERROR``.                                       |
+---------------+---------------------------------------------------------------+
| secret\_ref   | Unique identifier for the secret. This value is assigned by   |
|               | the API.                                                      |
+---------------+---------------------------------------------------------------+
| secret\_type  | The secret type. The possible secret types are as follows:    |
|               |                                                               |
|               |     - ``symmetric``: Used for storing byte arrays such as     |
|               |       keys suitable for symmetric encryption.                 |
|               |     - ``public``: Used for storing the public key of an       |
|               |       asymmetric key pair.                                    |
|               |     - ``private``: Used for storing the private key of an     |
|               |       asymmetric key pair.                                    |
|               |     - ``passphrase``: Used for storing plain-text             |
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
| expiration    | The expiration date for the secret in ISO-8601 format. After  |
|               | the secret has expired, it is no longer be returned by the    |
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
   the secret metadata and the payload in the JSON request body as shown
   in the :ref:`Store a secret <gsg-store-a-secret>` example.

-  Submit a **POST** request without a ``payload`` attribute against the
   secrets resource and then include the payload in a subsequent **PUT**
   request against the secret that was created by the POST. This mode enables
   you to upload payloads that cannot be included inside the JSON body, such
   as a binary file, to the |product name| system directly for encrypted
   storage. See the
   :ref:`Create and store a secret by using two requests
   <gsg-two-step-secret-creation>` example.


.. _containers-concept:

Container
~~~~~~~~~

A *container* is a logical object that you can use to store reference links to
secret resources that are related by relationship or type. For example, you can
create a single container to group secrets for a private key, certificate, and
intermediate certificate bundle for a TLS certificate.

|product name| supports the following types of containers:

.. contents::
   :local:
   :depth: 1

.. _generic_containers:

Generic containers
------------------

A generic container is used to hold any type or number of secrets. There are no
restrictions on the type or number of secrets that can be held within a
generic container.

An example of a use case for a generic container is storing multiple
passwords in the same container reference, as shown in the following example:

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

Certificate containers
----------------------

A certificate container is used to store X.509 Certificates with other secrets
that are needed to successfully use the certificate.  Other secrets can be
any of the following types:

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

The payload for the secret referenced as the ```certificate`` is expected to
be a PEM formatted X.509 certificate.

The payload for the secret referenced as the ```intermediates`` is expected to
be a PEM formatted PKCS#7 certificate chain.

The payload for the secret referenced as the ```private_key`` is expected to
be a PKCS#8 RSA private key.


.. _rsa_containers:

RSA containers
--------------

An RSA containers is used to store RSA public keys, and their associated
private keys, and private key passphrases.

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
~~~~~~

All users authenticated with |product name| can read the effective quota values
that apply to their account. |product name| identifies the account for a user
based on the data included in the authentication token.

Quotas are enforced for the following |product name| resources: secrets,
containers, and consumers.  The following table describes the possible values
for the quota attribute.

.. csv-table::
   :header: "Value", "Description"
   :widths: 15, 40

   "Any positive integer", "Defines the maximum number of resources allowed for your account"
   "0", "Indicates that a resource has been effectively disabled"
   "-1", "Indicates that the account has no limits on the number of resources you can
   create."

If you want to raise the quota limits on your account, contact
`Rackspace Cloud support`_.

.. _Rackspace Cloud support: https://www.rackspace.com/en-us/support#cloud


.. _consumer_concept:

Consumer
~~~~~~~~

A *consumer* is registered as an interested party for a container. For example,
when a Load Balancer uses a certificate bundle stored in |product name|, the
load balancer registers itself as a consumer of the certificate container. You
can view all of the registered consumers of a container by submitting a
:ref:`retrieve consumers <get-containers-consumers>` API request.

To prevent unexpected service problems, notify all consumers before you delete
a container.
