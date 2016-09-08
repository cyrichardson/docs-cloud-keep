
.. _post-consumers:

Create a consumer
~~~~~~~~~~~~~~~~~

.. code::

    POST /{version}/containers/{container_id}/consumers

This operation creates a consumer for the specified container.

The following table shows the possible response codes for this operation.

+------+-----------------------------------------------------------------------------+
| Code | Description                                                                 |
+======+=============================================================================+
| 201  | Successful creation of the consumer                                         |
+------+-----------------------------------------------------------------------------+
| 401  | Invalid X-Auth-Token or the token doesn't have permissions to this resource |
+------+-----------------------------------------------------------------------------+
| 403  | Forbidden.  The user has been authenticated, but is not authorized to       |
|      | create a consumer.  This can be based on the the user's role or the         |
|      | project's quota.                                                            |
+------+-----------------------------------------------------------------------------+


Request
-------

The following table shows the URI parameters for this request.

+-------------------+---------+--------------------------------------------+
|Parameter name     |Type     |Description                                 |
+===================+=========+============================================+
|container_id       | string  | The UUID for the container                 |
+-------------------+---------+--------------------------------------------+


The following table shows the body parameters for the request.

+-------------------+---------+--------------------------------------------+
|Parameter name     |Type     |Description                                 |
+===================+=========+============================================+
|name               | string  | The name of the consumer set by the user.  |
+-------------------+---------+--------------------------------------------+
|URL                | string  | The URL for the user or service using the  |
|                   |         | container.                                 |
+-------------------+---------+--------------------------------------------+


**Example: Create a consumer, cURL request**


.. code::

      curl -X POST -H 'X-Auth-Token $AUTH-TOKEN' \
           -H 'Content-Type: application/json' \
           -d '{
                 "name": "your consumer name",
                  "URL": "{consumerURL}"
              }' \
           $ENDPOINT/v1/containers/{container_id}/consumers


Response
--------

The following table shows the response attributes.

+-------------+---------+---------------------------------------------------------------+
| Name        | Type    | Description                                                   |
+=============+=========+===============================================================+
|**status**   | string  | Returns the current state for the specified consumer          |
+-------------+---------+---------------------------------------------------------------+
|**updated**  | date    | The date and time that the consumer was last updated.         |
+-------------+---------+---------------------------------------------------------------+
|**name**     | string  | The name of the container that the user is registering for    |
+-------------+---------+---------------------------------------------------------------+
|**consumers**| dict    | Returns a dictionary of information for the                   |
|             |         | consumer resource.                                            |
+-------------+---------+---------------------------------------------------------------+
|consumers.\  | string  | Returns the URL for the user or service using the container.  |
|**URL**      |         | for the containers resource. In the response example, the     |
|             |         | consumer URL is ``https://consum.er``.                        |
+-------------+---------+---------------------------------------------------------------+
|consumers.\  | string  | The name of the consumer set by the user.                     |
|**name**     |         |                                                               |
+-------------+---------+---------------------------------------------------------------+


**Example: Create a consumer, JSON response**


.. code::

    {
        "status": "ACTIVE",
        "updated": "2015-10-15T17:56:18.626724",
        "name": "your container name",
        "consumers": [
            {
                "URL": "https://consum.er",
                "name": "your consumer name"
            }
    }
