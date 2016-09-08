
.. _post-container:

Create a container
~~~~~~~~~~~~~~~~~~

.. code::

    POST /{version}/containers

This operation creates a container.You can create the following types of
containers: generic, RSA, and certificate.

**Generic**
   This type of container holds references to any type or number of secrets.
   Each secret reference is accompanied by a name. Unlike other container
   types, no specific restrictions are enforced on the ``name`` attribute.

**RSA**
   This type of container is used to hold references to only the following
   types of secrets, which are enforced by the their names:
   ``public_key``, ``private_key``, and ``private_key_passphrase``.

**Certificate**
   This type of container is used to hold a reference to a certificate and
   optionally private key, private key passphrase, and intermediates.


The following table shows the possible response codes for this operation.

+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 201  | Successful creation of the container                                        |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 403  | Forbidden.  The user has been authenticated, but is not authorized to       |
|      | create a container.  This can be based on the the user's role or the        |
|      | project's quota.                                                            |
+------+-----------------------------------------------------------------------------+

Request
-------

There are no URL parameters for this request.

The following table shows the body parameters for the request:

+----------------+--------+--------------------------------------------------------+
| Name           | Type   | Description                                            |
+================+========+========================================================+
|**type**        | string | Type of container. Possible values are  ``generic``,   |
|                |        | ``rsa``, and ``certificate``.                          |
+----------------+--------+--------------------------------------------------------+
|**name**        | string | *(Optional)* Human readable name for identifying your  |
|                |        | container.                                             |
+----------------+--------+--------------------------------------------------------+
|**secret_refs** | list   | A list of dictionaries that contain references to      |
|                |        | secrets.                                               |
+----------------+--------+--------------------------------------------------------+
|secret_refs.\   | string |The name assigned to the secret resource when it was    |
|**name**        |        |created.                                                |
+----------------+--------+--------------------------------------------------------+
|secret_refs.\   | URI    | A HATEOAS URL to retrieve information about the        |
|**secret_ref**  |        | specified secret.                                      |
+----------------+--------+--------------------------------------------------------+
|**secretID**    | string | The UUID for the secret to be added to the container.  |
+----------------+--------+--------------------------------------------------------+


**Example: Create a container, cURL request**


.. code::

      curl -X POST -H 'X-Auth-Token $AUTH-TOKEN -d \
        '{
            "type": "generic",
            "name": "container name",
            "secret_refs": [
                {
                    "name": "private_key",
                    "secret_ref": "$ENDPOINT/v1/secrets/{secretID}"
                }
            ]
        }' $ENDPOINT/v1/containers


Response
--------

The following table shows the response attributes.

+-------------------+---------+----------------------------------------------------+
| Parameter name    | Type    | Description                                        |
+===================+=========+====================================================+
|**container_ref**  | URI     |Returns a HATEOS URL to retrieve information        |
|                   |         |about the container resource.                       |
+-------------------+---------+----------------------------------------------------+
|containerID        | string  | The UUID value assigned to the container.          |
|                   |         | In the follwoing example, the container ID is      |
|                   |         | ``6ad67bc0-17fd-45ce-b84a-a9be44fe06``.            |
+-------------------+---------+----------------------------------------------------+


**Example: Create a container, JSON response**


.. code::

   {
       "container_ref": "https://iad.keep.api.rackspacecloud.com/v1/containers/6ad67bc0-17fd-45ce-b84a-a9be44fe069b"
   }
