
.. _get-orders:

Get Orders
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/{tenantId}/orders

This method lists all orders for a specified tenant. Performing a GET on the secrets 
resource with no UUID retrieves a batch of the most recent orders per the requesting 
tenant. 				

The retrieved list of orders is ordered by oldest to newest created date.

The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |Success                  |This status code is      |
|                          |                         |returned when the orders |
|                          |                         |have been successfully   |
|                          |                         |retrieved.               |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""


The following table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{tenantId}                |String *(Required)*      |This parameter specifies |
|                          |                         |the tenant ID of the     |
|                          |                         |client subscribing to    |
|                          |                         |the Barbican service     |
+--------------------------+-------------------------+-------------------------+


This operation does not accept a request body.


**Example: Get orders cURL request**


.. code::

   curl -H 'Accept: application/json' \
        -H 'X-Project-Id:12345'\
        $ENDPOINT/orders


Response
""""""""""""""""

**Example: Get order JSON response**


.. code::

   {
       "total": 15,
       "orders": [
           {
               "status": "ACTIVE",
               "updated": "2014-08-25T20:43:01.563865",
               "created": "2014-08-25T20:42:59.793193",
               "order_ref": "https://endpointURL/v1/orders/c8a154dc-5816-49ac-9016-6a9030fc2449",
               "secret_ref": "https://endpointURL/v1/secrets/15108db8-4505-4c5b-96b9-a9838951f28f",
               "secret": {
                   "name": "secretname",
                   "algorithm": "aes",
                   "payload_content_type": "application/octet-stream",
                   "expiration": null,
                   "bit_length": 256,
                   "mode": "cbc"
               },
               "meta": null,
               "type": "key"
           },
           {
               "status": "ACTIVE",
               "updated": "2014-08-25T21:18:35.886867",
               "created": "2014-08-25T21:18:33.484137",
               "order_ref": "https://endpointURL/v1/orders/240e7679-4178-43fd-b673-96fa73f33598",
               "secret_ref": "https://endpointURL/v1/secrets/f74a51d2-99a8-423a-8cea-2bf10b263584",
               "secret": {
                   "name": "secretname",
                   "algorithm": "aes",
                   "payload_content_type": "application/octet-stream",
                   "expiration": null,
                   "bit_length": 256,
                   "mode": "cbc"
               },
               "meta": null,
               "type": "key"
           },
           {
               "status": "ACTIVE",
               "updated": "2014-08-25T21:31:07.622288",
               "created": "2014-08-25T21:31:07.395485",
               "order_ref": "https://endpointURL/v1/orders/af64236a-ba34-4fa5-96ad-c112a662de65",
               "secret_ref": "https://endpointURL/v1/secrets/5fca3629-9f78-4e23-b5ab-15497043c867",
               "secret": {
                   "name": "secretname",
                   "algorithm": "aes",
                   "payload_content_type": "application/octet-stream",
                   "expiration": null,
                   "bit_length": 256,
                   "mode": "cbc"
               },
               "meta": null,
               "type": "key"
           }
       ],
       "next": "https://endpointURL/v1/orders?limit=10&offset=10"
