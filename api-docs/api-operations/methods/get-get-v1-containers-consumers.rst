
.. _get-containers-consumers:

Get a container's consumers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/containers/{container_ref}/consumers


Lists a container's consumers.

The list of consumers can be filtered by the parameters passed in via the URL.

The following table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |This status code is      |
|                          |                         |returned when the        |
|                          |                         |consumers have been      |
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

+--------------+------------+------------------------------------------------------------+
| Name         | Type       | Description                                                |
+==============+============+============================================================+
|{containerID} |integer     | The UUID for the container you would like to retrieve.     |
+--------------+------------+------------------------------------------------------------+
|{offset}      |integer     | The starting index within the total list of the consumers  |
|              |*(Optional)*| that you would like to retrieve.                           |
+--------------+------------+------------------------------------------------------------+
|{limit}       |integer     | The maximum number of records to return (up to 100). The   |
|              |*(Optional)*| default limit is 10.                                       |
+--------------+------------+------------------------------------------------------------+


**Example: Get consumers for a container cURL request**


.. code::

    curl -H 'Accept: application/json' -H 'X-Auth-Token:$AUTH-TOKEN'\
    $ENDPOINT/v1/containers/{containerID}/consumers/?offset={offset}&limit={limit}


Response
""""""""""""""""

The following table shows the response parameters for this request.

+-------------+---------+---------------------------------------------------------------+
| Name        | Type    | Description                                                   |
+=============+=========+===============================================================+
|**total**    | integer | Returns the number of consumers in the specified container.   |
+-------------+---------+---------------------------------------------------------------+
|**consumers**| dict    | Returns a dictionary of consumer information for the specified|
|             |         | consumers resource.                                           |
+-------------+---------+---------------------------------------------------------------+
|consumers.\  | string  | Returns the current state for the specified consumer          |
|**status**   |         |                                                               |    
+-------------+---------+---------------------------------------------------------------+
|consumers.\  | string  | Returns the URL for the user or service using the container.  |
|**URL**      |         | for the containers resource.                                  |
+-------------+---------+---------------------------------------------------------------+
|consumers.\  | date    | The date and time that the consumer was last updated.         |
|**updated**  |         |                                                               |
+-------------+---------+---------------------------------------------------------------+
|consumers.\  | string  | The name of the consumer set by the user.                     |
|**name**     |         |                                                               |
+-------------+---------+---------------------------------------------------------------+
|consumers.\  | date    | The date and time that the consumer was created.              |
|**created**  |         | consumers resource.                                           |
+-------------+---------+---------------------------------------------------------------+
|consumers.\  | URI     | A HATEOAS url to retrieve the next set of consumers based on  |
|**next**     |         | the offset and limit parameters. This attribute is only       |
|             |         | available when the total number of consumers is greater than  |
|             |         | offset and limit parameter combined.                          |
+-------------+---------+---------------------------------------------------------------+
|consumers.\  | string  | A HATEOAS url to retrieve the previous set of consumers based |
|**previous** |         | on the offset and limit parameters. This attribute is only    |
|             |         | available when the request offset is greater than 0.          |
+-------------+---------+---------------------------------------------------------------+


**Example: Get consumers for a specified container JSON response**


.. code::

      {
        "total": 3,
        "consumers": [
          {
              "status": "ACTIVE",
              "URL": "consumerurl",
              "updated": "2015-10-15T21:06:33.123878",
              "name": "consumername",
              "created": "2015-10-15T21:06:33.123872"
          },
          {
              "status": "ACTIVE",
              "URL": "consumerURL2",
              "updated": "2015-10-15T21:17:08.092416",
              "name": "consumername2",
              "created": "2015-10-15T21:17:08.092408"
          },
          {
              "status": "ACTIVE",
              "URL": "consumerURL3",
              "updated": "2015-10-15T21:21:29.970370",
              "name": "consumername3",
              "created": "2015-10-15T21:21:29.970365"
          }
        ]
      }

**Example: Get consumers for container with offset and limit parameters JSON response**

.. code::

     {
         "total": 3,
         "next": "https://iad.keep.api.rackspacecloud.com/v1/containers/6ad67bc0-17fd-45ce-b84a-a9be44fe069b/consumers?limit=1&offset=2",
         "consumers": [
            {
                "status": "ACTIVE",
                "URL": "consumerURL2",
                "updated": "2015-10-15T21:17:08.092416",
                "name": "consumername2",
                "created": "2015-10-15T21:17:08.092408"
            }
        ],
        "previous": "https://iad.keep.api.rackspacecloud.com/v1/containers/6ad67bc0-17fd-45ce-b84a-a9be44fe069b/consumers?limit=1&offset=0"
     }

