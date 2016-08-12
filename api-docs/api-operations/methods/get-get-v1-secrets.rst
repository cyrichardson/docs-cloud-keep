
.. _get-secrets:

Get Secrets
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v1/secrets

This method retrieves all secrets for your account.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |This status code is      |
|                          |                         |returned when the        |
|                          |                         |secrets have been        |
|                          |                         |successfully retrieved   |
|                          |                         |for the tenant.          |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |This status code is      |
|                          |                         |returned when the        |
|                          |                         |user was not succesfully |
|                          |                         |authenticated.           |
+--------------------------+-------------------------+-------------------------+
|403                       |Forbidden                |This status code is      |
|                          |                         |returned when the        |
|                          |                         |user does not have the   |
|                          |                         |correct RBAC role(s).    |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""

The following table shows the URI parameters for the request:

+-------------+---------+-----------------------------------------------------------------+
| Name        | Type    | Description                                                     |
+=============+=========+=================================================================+
| offset      | integer | The starting index within the total list of the secrets that    |
|             |         | you would like to retrieve.                                     |
+-------------+---------+-----------------------------------------------------------------+
| limit       | integer | The maximum number of records to return (up to 100). The        |
|             |         | default limit is 10.                                            |
+-------------+---------+-----------------------------------------------------------------+
| name        | string  | Selects all secrets with name similar to this value.            |
+-------------+---------+-----------------------------------------------------------------+
| secret_type | string  | Selects all secrets with secret_type equal to this value.       |
+-------------+---------+-----------------------------------------------------------------+
| acl_only    | boolean | Selects all secrets with an ACL that contains the user.         |
|             |         | Project scope is ignored.                                       |
+-------------+---------+-----------------------------------------------------------------+
| created     | string  | Date filter to select all secrets with `created` matching the   |
|             |         | specified criteria.  See Date Filters below for more detail.    |
+-------------+---------+-----------------------------------------------------------------+
| updated     | string  | Date filter to select all secrets with `updated` matching the   |
|             |         | specified criteria. See Date Filters below for more detail.     |
+-------------+---------+-----------------------------------------------------------------+
| expiration  | string  | Date filter to select all secrets with `expiration` matching    |
|             |         | the specified criteria. See Date Filters below for more detail. |
+-------------+---------+-----------------------------------------------------------------+
| sort        | string  | Determines the sorted order of the returned list.  See Sorting  |
|             |         | below for more detail.                                          |
+-------------+---------+-----------------------------------------------------------------+
| alg         | string  | (Deprecated) Selects all secrets with their algorithm metadata  |
|             |         | attribute similar to this value.                                |
+-------------+---------+-----------------------------------------------------------------+
| mode        | string  | (Deprecated) Selects all secrets with their mode metadata       |
|             |         | attribute similar to this value.                                |
+-------------+---------+-----------------------------------------------------------------+
| bits        | integer | (Deprecated) Selects all secrets with their bit_length metadata |
|             |         | attribute equal to this value.                                  |
+-------------+---------+-----------------------------------------------------------------+

This operation does not take a request body.


**Example: Get secret list cURL request**

.. code::

   curl -H 'Accept: application/json' \
        -H "X-Auth-Token: $AUTH_TOKEN" \
        "$ENDPOINT/v1/secrets?offset=1&limit=3&secret_type=passphrase"


Date Filters
""""""""""""""""

The values for the ``created``, ``updated``, and ``expiration`` parameters are
comma-separated lists of time stamps in ISO 8601 format.  The time stamps can
be prefixed with any of these comparison operators: ``gt`` (greater-than),
``gte`` (greater-than-or-equal), ``lt`` (less-than), ``lte`` (less-than-or-equal).

For example, submit the following request to get a list of secrets that expire
in January 2020:

.. code::

   curl -H 'Accept: application/json' \
        -H "X-Auth-Token: $AUTH_TOKEN" \
        $ENDPOINT/v1/secrets?expiration=gte:2020-01-01T00:00:00,lt:2020-02-01T00:00:00


Sorting
""""""""""""""""

The value of the ``sort`` parameter is a comma-separated list of sort keys.
Supported sort keys include ``created``, ``expiration``, ``mode``, ``name``,
``secret_type``, ``status``, and ``updated``.

Each sort key may also include a direction.  Supported directions
are ``:asc`` for ascending and ``:desc`` for descending.  The service will
use ``:asc`` for every key that does not include a direction.

For example, submit the following request to sort the list from the most
recently created to the oldest:

.. code::

   curl -H 'Accept: application/json' \
        -H "X-Auth-Token: $AUTH_TOKEN" \
        $ENDPOINT/v1/secrets?sort=created:desc


Response
""""""""""""""""


The following table shows the response atttributes for the request:

+------------+---------+--------------------------------------------------------+
| Name       | Type    | Description                                            |
+============+=========+========================================================+
| secrets    | list    | Contains a list of dictionaries filled with secret     |
|            |         | data                                                   |
+------------+---------+--------------------------------------------------------+
| total      | integer | The total number of secrets available to the user      |
+------------+---------+--------------------------------------------------------+
| next       | string  | A HATEOAS url to retrieve the next set of secrets      |
|            |         | based on the offset and limit parameters. This         |
|            |         | attribute is only available when the total number of   |
|            |         | secrets is greater than offset and limit parameter     |
|            |         | combined.                                              |
+------------+---------+--------------------------------------------------------+
| previous   | string  | A HATEOAS url to retrieve the previous set of          |
|            |         | secrets based on the offset and limit parameters.      |
|            |         | This attribute is only available when the request      |
|            |         | offset is greater than 0.                              |
+------------+---------+--------------------------------------------------------+

The following response examples show the results of sending an API request with
an offset value of 0 and a limit value of 3.

**Example: Get secrets JSON response**


.. code::

    {
        "secrets": [
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
        "next": "https://iad.keep.api.rackspacecloud.com/v1/secrets?limit=3&offset=3"
    }
