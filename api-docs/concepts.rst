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
  * Private Key
  * Certificate
  * Password
  * SSH Keys

The secret schema represents the actual secret or key that is presented
to the |product name| service.  Secrets themselves can be any format.

The following example shows the specification for a secret that has been added to |product name|:

.. code::

    {
        "uuid": "e2b633c7-fda5-4be8-b42c-9a2c9280284d",
        "name": "AES key",
        "expiration": "2018-02-28T19:14:44.180394",
        "secret": "b7990b786ee9659b43e6b1cd6136de07d9c5…",
        "secret_type": "application/aes-256-cbc",
      }

A secret consists of the following elements:

+--------------+---------------------------------------------------------------+
| Element      | Description                                                   |
+==============+===============================================================+
| uuid         | Unique identifier for the secret. This value is assigned by   |
|              | the API.                                                      |
+--------------+---------------------------------------------------------------+
| name         | Human readable name for the secret.                           |
+--------------+---------------------------------------------------------------+
| expiration   | The expiration date for the secret in ISO-8601 format. Once   |
|              | the secret has expired, it will no longer be returned by the  |
|              | API or agent.                                                 |
+--------------+---------------------------------------------------------------+
| secret       | The base64-encoded value of the secret.                       |
+--------------+---------------------------------------------------------------+
| secret\_type | (optional) The secret type. The possible secret types are:    |
|              |                                                               |
|              |         - symmetric: Used for storing byte arrays such as     |
|              |           keys suitable for symmetric encryption.             |
|              |         - public: Used for storing the public key of an       |
|              |           asymmetric keypair.                                 |
|              |         - private: Used for storing the private key of an     |
|              |           asymmetric keypair.                                 |
|              |         - passphrase: Used for storing plain text             |
|              |           passphrases.                                        |
|              |         - certificate: Used for storing cryptographic         |
|              |           certificates such as X.509 certificates.            |
|              |                                                               |
+--------------+---------------------------------------------------------------+


You can use one of the following methods to store a secret:

-  Submit a **POST** request against the secrets resource. Include
   the secret metadata in the JSON body and include the secret itself
   in the ``payload`` parameter.

-  Submit a **POST** request without a ``payload`` parameter against the
   secrets resource and then include the payload in a subsequent **PUT**
   request. This mode enables you to upload a binary file to the
   |product name| database directly for encrypted storage.

..  note::
        Note
        Submitting a **POST** request creates secret metadata. If the payload is
        provided with the **POST** request, then it is encrypted and stored, and
        then linked with this metadata. If no payload is included with the
        **POST** request, it must be provided with a subsequent **PUT** request.
        The secret resource encrypts and stores client-provided secret
        information and metadata.


.. _Barbican-dg-containers:

Container
~~~~~~~~~~~~~~~~~~

The containers resource is the organizational center piece of |product name| that simplifies secrets management
in environments that have large numbers of secrets.

A container is a logical object that can be used to store secret references that are related by relationship or type. 
For example you can create a single container to group a private key, certificate, and bundle for
an SSL certificate. Containers simplify the task of managing large numbers of secrets resources.

|product name| supports 3 types of containers:
  * :ref:`Generic <generic_containers>`
  * :ref:`Certificate <certificate_containers>`
  * :ref:`RSA <rsa_containers>`

Each of these types have explicit restrictions as to what type of secrets should be
held within. These will be broken down in their respective sections.

This guide assumes that you are running |product name| in a local development environment.


.. _generic_containers:

Generic Containers
######################

A generic container is used for any type of container that a user may wish to create.
There are no restrictions on the type or amount of secrets that can be held within a container.

An example of a use case for a generic container would be having multiple passwords stored
in the same container reference:

.. code-block:: json

    {
        "type": "generic",
        "status": "ACTIVE",
        "name": "Test Environment User Passwords",
        "consumers": [],
        "container_ref": "https://{cloudkeep_host}/v1/containers/{container_uuid}",
        "secret_refs": [
            {
                "name": "test_admin_user",
                "secret_ref": "https://{cloudkeep_host}/v1/secrets/{secret1_uuid}"
            },
            {
                "name": "test_audit_user",
                "secret_ref": "https://{cloudkeep_host}/v1/secrets/{secret2_uuid}"
            }
        ],
        "created": "2015-03-30T21:10:45.417835",
        "updated": "2015-03-30T21:10:45.417835"
    }


.. _certificate_containers:

Certificate Containers
##########################

A certificate container is used for storing the following secrets that are relevant to
certificates:

  * certificate
  * private_key (optional)
  * private_key_passphrase (optional)
  * intermediates (optional)

.. code-block:: json

    {
        "type": "certificate",
        "status": "ACTIVE",
        "name": "Example.com Certificates",
        "consumers": [],
        "container_ref": "https://{cloudkeep_host}/v1/containers/{container_uuid}",
        "secret_refs": [
            {
                "name": "certificate",
                "secret_ref": "https://{cloudkeep_host}/v1/secrets/{cert_uuid}"
            },
            {
                "name": "private_key",
                "secret_ref": "https://{cloudkeep_host}/v1/secrets/{pk_uuid}"
            },
            {
                "name": "private_key_passphrase",
                "secret_ref": "https://{cloudkeep_host}/v1/secrets/{pass_uuid}"
            },
            {
                "name": "intermediates",
                "secret_ref": "https://{cloudkeep_host}/v1/secrets/{inters_uuid}"
            }

        ],
        "created": "2015-03-30T21:10:45.417835",
        "updated": "2015-03-30T21:10:45.417835"
    }

The payload for the secret referenced as the "certificate" is expected to be a
PEM formatted x509 certificate.

The payload for the secret referenced as the "intermediates" is expected to be a
PEM formatted PKCS7 certificate chain.


.. _rsa_containers:

RSA Containers
#######################

An RSA container is used for storing RSA public keys, private keys, and private
key pass phrases.

.. code-block:: json

    {
        "type": "rsa",
        "status": "ACTIVE",
        "name": "John Smith RSA",
        "consumers": [],
        "container_ref": "https://{cloudkeep_host}/v1/containers/{container_uuid}",
        "secret_refs": [
            {
                "name": "private_key",
                "secret_ref": "https://{cloudkeep_host}/v1/secrets/{pk_uuid}"
            },
            {
                "name": "private_key_passphrase",
                "secret_ref": "https://{cloudkeep_host}/v1/secrets/{pass_uuid}"
            },
            {
                "name": "public_key",
                "secret_ref": "https://{cloudkeep_host}/v1/secrets/{pubkey_uuid}"
            }

        ],
        "created": "2015-03-30T21:10:45.417835",
        "updated": "2015-03-30T21:10:45.417835"
    }


.. _Barbican-dg-quotas:

Quotas
~~~~~~~~~~~~~~~~~~

All users authenticated with |product name| are able to read the effective quota values
that apply to their project. |product name| can derive the project that a user belongs
to by reading the project scope from the authentication token.

Service administrators can read, set, and delete quota configurations for each
project known to |product name|.  These operations are available to an authenticated user
that has the service administrator role. This role is defined in the |product name| policy.json configuration file.

The name for a service administrator role is "keep:service-admin".

Quotas can be enforced for the following |product name| resources: secrets, containers,
and consumers.  The configured quota value can be 

- -1 meaning no limit to the number of resources you can create
- 0 meaning this resource has been disabled
- positive integer defining the maximum number allowed for a project
  
If no value is specified, |product name| uses the default setting, and the quota value is set to None.

.. _default_project_quotas:

Default Quotas
################

When no project quotas have been set for a project, the default
project quotas are enforced for that project.  Default quotas are specified
in the |product name| configuration file (barbican.conf).  The defaults provided
in the standard configuration file are as follows.

.. code-block:: none

    # default number of secrets allowed per project
    quota_secrets = -1

    # default number of containers allowed per project
    quota_containers = -1

    # default number of consumers allowed per project
    quota_consumers = -1


The default quotas are returned via a **GET** on the **quotas** resource when no
explicit project quotas have been set for the current project.



.. _Barbican-dg-consumer:


Consumer
~~~~~~~~~~~~~~~~~~

A consumer is a way to to register as an interested party for a container.
All of the registered consumers can be viewed by performing a **GET** on the
{container_ref}/consumers resource. Before a container is deleted, all consumers
should be notified of the delete.
