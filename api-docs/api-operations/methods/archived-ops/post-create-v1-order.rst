
.. _post-order:

Create Order
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /{version}/{tenantId}/orders

This method creates an order.

This method creates a new order.


The following table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|201                       |Success                  |This status code is      |
|                          |                         |returned when the order  |
|                          |                         |was successfully created.|
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned when the data   |
|                          |                         |provided in the POST     |
|                          |                         |request is invalid. This |
|                          |                         |can include schema       |
|                          |                         |violations such as the   |
|                          |                         |secret's mime-type not   |
|                          |                         |specified                |
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned when the value  |
|                          |                         |provided in the          |
|                          |                         |"payload_content_type"   |
|                          |                         |parameter is invalid.    |
|                          |                         |This is caused when thre |
|                          |                         |is no crypto plugin      |
|                          |                         |available that supports  |
|                          |                         |the payload_content_type |
|                          |                         |requested                |
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


The following table shows the body parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|\ **name**                |String *(Optional)*      |This parameter specifies |
|                          |                         |the name of the secret.  |
+--------------------------+-------------------------+-------------------------+
|\ **algorithm**           |String *(Optional)*      |Specifies the algorithm  |
|                          |                         |type used to store the   |
|                          |                         |secret. This parameter   |
|                          |                         |is optional.             |
+--------------------------+-------------------------+-------------------------+
|\ **bit_length**          |Integer *(Optional)*     |Specifies the bit length |
|                          |                         |of the secret. Must be a |
|                          |                         |positive integer. This   |
|                          |                         |parameter is optional.   |
+--------------------------+-------------------------+-------------------------+
|\ **mode**                |String *(Optional)*      |Specifies the type/mode  |
|                          |                         |of the algorithm         |
|                          |                         |associated with the      |
|                          |                         |secret information. This |
|                          |                         |parameter is optional.   |
+--------------------------+-------------------------+-------------------------+
|\ **payload_content_type**|String *(Optional)*      |Specifies the            |
|                          |                         |type/format the secret   |
|                          |                         |data is provided in.     |
+--------------------------+-------------------------+-------------------------+


**Example:Create Order: JSON request**


.. code::

   curl -X POST -d \
    '{
      "secret":
   	       {
   		"name": "secretname",
   		 "algorithm": "aes",
   		 "bit_length": 256,
   		 "mode": "cbc",
   		 "payload_content_type": "application/octet-stream"
   		}
   }'\
   https://endpointURL/v1/12345/orders


Response
""""""""""""""""


**Example:Create Order: JSON response**


.. code::

   {
    "order_ref": "https://endpointURL/v1/12345/orders/62d57f53-ecfe-4ae4-87bd-fab2f24e29bc"
   }
