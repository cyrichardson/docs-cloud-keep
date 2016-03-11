
.. _get-secrets:

Get Secrets
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/secrets

This method retrieves all secrets for a given tenant.



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

+--------+---------+------------------------------------------------------------+
| Name   | Type    | Description                                                |
+========+=========+============================================================+
| offset | integer | The starting index within the total list of the secrets    |
|        |         | that you would like to retrieve.                           |
+--------+---------+------------------------------------------------------------+
| limit  | integer | The maximum number of secrets to return (up to 100).       |
|        |         | The default limit is 10.                                   |
+--------+---------+------------------------------------------------------------+

This operation does not take a request body.


**Example: Delete secret cURL request**


.. code::

   curl -H 'Accept: application/json' \
        -H 'X-Auth-Token: $AUTH-TOKEN' \
        $ENDPOINT/v1/secrets?offset={offset}&limit={limit}


Response
""""""""""""""""


The following table shows the response parameters for the request:

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

The following response examples shows the resutls of sending an API request where the 
offset is 0 and the limit is 2. 

**Example: Get secrets JSON response**


.. code::

   {
       "secrets": [
           {
               "status": "ACTIVE",
               "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/15108db8-4505-4c5b-96b9-a9838951f28f",
               "updated": "2014-08-25T20:43:01.510569",
               "name": "secretname",
               "algorithm": "aes",
               "created": "2014-08-25T20:43:01.421625",
               "content_types": {
                   "default": "application/octet-stream"
               },
               "mode": "cbc",
               "bit_length": 256,
               "expiration": null
           },
           {
               "status": "ACTIVE",
               "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/485950f0-37a5-4ba4-b1d6-413f79b849ef",
               "updated": "2014-08-25T21:18:35.821340",
               "name": "secretname",
               "algorithm": "aes",
               "created": "2014-08-25T21:18:35.719952",
               "content_types": {
                   "default": "application/octet-stream"
               },
               "mode": "cbc",
               "bit_length": 256,
               "expiration": null
           }
       ],
       "total": 2,
       "next": "https://iad.keep.api.rackspacecloud.com/v1/secrets?limit=2&offset=3",
       "previous": "https://iad.keep.api.rackspacecloud.com/v1/secrets?limit=2&offset=0"
   }

