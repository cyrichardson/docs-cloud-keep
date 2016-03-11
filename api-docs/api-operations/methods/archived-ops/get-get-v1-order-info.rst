
.. _get-order-information:

Get Order Information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /{version}/{tenantId}/orders/{order_id}

This method retrieves information about a specified order.

This method retrieves information for the specified order including g a link to the 
secret that was stored as a result of the order (if available).


The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |Success                  |This status code is      |
|                          |                         |returned when the order  |
|                          |                         |info was successfully    |
|                          |                         |retrieved.               |
+--------------------------+-------------------------+-------------------------+
|404                       |Error                    |This error code is       |
|                          |                         |returned when the        |
|                          |                         |supplied UUID doesn't    |
|                          |                         |match an order in the    |
|                          |                         |data store, which means  |
|                          |                         |the order doesn't exist. |
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
|{orderid}                 |String                   |Specifies the unique     |
|                          |                         |identifier of an order   |
|                          |                         |that has been created.   |
+--------------------------+-------------------------+-------------------------+



This operation does not accept a request body.




**Example: Get Order Information cURL request**


.. code::

   curl -H 'Accept: application/json'\
        $ENDPOINT/v1/12345/orders/62d57f53-ecfe-4ae4-87bd-fab2f24e29bc



Response
""""""""""""""""


**Example: Get order information JSON response**


.. code::

   {
       "status": "ACTIVE",
       "secret_ref": "endpointURL/v1/12345/secrets/8a78d5e4-524a-4e81-96cc-c7d16ed85515",
       "updated": "2014-04-02T14:52:26.987458",
       "created": "2014-04-02T14:52:26.921043",
       "secret": {
           "name": "secretname",
           "algorithm": "aes",
           "payload_content_type": "application/octet-stream",
           "expiration": null,
           "bit_length": 256,
           "mode": "cbc"
            },
       "order_ref": "https://endpointURL/v1/12345/orders/b63d2c05-5d53-4db6-af06-4e388044deb8"
