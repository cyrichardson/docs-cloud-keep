
.. _get-containers:

Retrieve containers
~~~~~~~~~~~~~~~~~~~

.. code::

    GET /{version}/containers

This operation retrieves a list of the containers in a project.
Returned containers are ordered by creation date; oldest to newest.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |This status code is      |
|                          |                         |returned when the        |
|                          |                         |containers have been     |
|                          |                         |successfully retrieved   |
|                          |                         |for the tenant.          |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |This status code is      |
|                          |                         |returned when the        |
|                          |                         |user was not successfully|
|                          |                         |authenticated.           |
+--------------------------+-------------------------+-------------------------+
|403                       |Forbidden                |This status code is      |
|                          |                         |returned when the        |
|                          |                         |user does not have the   |
|                          |                         |correct RBAC role or     |
|                          |                         |roles.                   |
+--------------------------+-------------------------+-------------------------+


Request
-------

The following table shows the URI parameters for the request.

+--------+---------+------------------------------------------------------------+
| Name   | Type    | Description                                                |
+========+=========+============================================================+
| offset | integer | The starting index within the total list of the containers |
|        |         | that you want to retrieve.                                 |
+--------+---------+------------------------------------------------------------+
| limit  | integer | The maximum number of containers to return (up to 100).    |
|        |         | The default limit is 10.                                   |
+--------+---------+------------------------------------------------------------+


This operation does not accept a request body.


**Example: Retrieve containers, cURL request**


.. code::

    curl -H 'Accept: application/json' \
         -H 'X-Auth-Token:$AUTH-TOKEN' \
         $ENDPOINT/v1/containers?offset={offset}&limit={limit}


Response
--------

The following table shows the response attributes.

+------------+---------+--------------------------------------------------------+
| Name       | Type    | Description                                            |
+============+=========+========================================================+
|containers  | list    | Returns a list of dictionaries with information about  |
|            |         | each container that has been created in Cloud Keep.    |
+------------+---------+--------------------------------------------------------+
|total       | integer | The total number of containers available to the user   |
+------------+---------+--------------------------------------------------------+
|next        | string  | A HATEOAS URL to retrieve the next set of containers   |
|            |         | based on the offset and limit parameters. This         |
|            |         | attribute is available only when the total number of   |
|            |         | containers is greater than the offset and limit        |
|            |         | parameter values combined.                             |
+------------+---------+--------------------------------------------------------+
|previous    | string  | A HATEOAS url to retrieve the previous set of          |
|            |         | containers based on the offset and limit parameters.   |
|            |         | This attribute is available only when the request      |
|            |         | offset is greater than 0.                              |
+------------+---------+--------------------------------------------------------+


**Example: Retrieve containers, JSON response**


.. code::

      {
        "containers": [
            {
                "consumers": [],
                "container_ref": "https://iad.keep.api.rackspacecloud.com/v1/containers/6ad67bc0-17fd-45ce-b84a-a9be44fe069b",
                "created": "2015-03-26T21:10:45.417835",
                "name": "container name",
                "secret_refs": [
                    {
                        "name": "private_key",
                        "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/485950f0-37a5-4ba4-b1d6-413f79b849ef"
                    }
                ],
                "status": "ACTIVE",
                "type": "generic",
                "updated": "2015-03-26T21:10:45.417835"
            }
        ],
        "total": 1
      }
