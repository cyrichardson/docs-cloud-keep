
.. _put-secret:

Update Secret
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    PUT /{version}/secrets/{secret_id}

This method stores the payload for an existing secret that was created without a payload.
To provide secret information after the secret is created, submit a PUT request to the 
URI that contains the secret ID of the secret you want to update. The PUT request should 
include the payload, as well as the appropriate Content-Type and Content-Encoding 
definitions.


.. note::

   You can only make PUT request once after a POST operation that does not 
   include a payload. Also note that you cannot modify any other attributes for 
   a secret resource by using the PUT operation.


The following table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No Content               |This status code is      |
|                          |                         |returned when the secret |
|                          |                         |has been successfully    |
|                          |                         |updated.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned when no crypto  |
|                          |                         |plugin supports the      |
|                          |                         |payload_content_type     |
|                          |                         |requested in the Content-|
|                          |                         |Type header.             |
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned when no value   |
|                          |                         |was provided for the     |
|                          |                         |"payload" parameter.     |
+--------------------------+-------------------------+-------------------------+
|404                       |Error                    |This error code is       |
|                          |                         |returned when the        |
|                          |                         |supplied UUID doesn't    |
|                          |                         |match a secret in the    |
|                          |                         |datastore for the        |
|                          |                         |specified tenant.        |
+--------------------------+-------------------------+-------------------------+
|409                       |Error                    |This error code is       |
|                          |                         |returned when the secret |
|                          |                         |already has encrypted    |
|                          |                         |data associated with it. |
+--------------------------+-------------------------+-------------------------+
|413                       |Error                    |This error code is       |
|                          |                         |returned when the secret |
|                          |                         |specified in the         |
|                          |                         |"payload" parameter is   |
|                          |                         |too large. The current   |
|                          |                         |size limit is 10,000     |
|                          |                         |bytes.                   |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""


The following table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{secret_id}               |String                   |This parameter specifies |
|                          |                         |the unique identifier of |
|                          |                         |a secret that has been   |
|                          |                         |stored.                  |
+--------------------------+-------------------------+-------------------------+
|{secretDataFile}          |Binary                   |A file containing the    |
|                          |                         |binary data to be stored | 
|                          |                         |as the secret payload.   |
+--------------------------+-------------------------+-------------------------+



This operation does not accept a request body.


**Example: Update secret cURL request**


.. code::

   curl -X PUT -H 'Content-Type: application/octet-stream' \
        -H 'X-Auth-Token: $AUTH-TOKEN' \
        -T {secretDataFile} $ENDPOINT/v1/secrets/a83018d1-e657-4957-9ddd-42a479753e6b


..  note::
    The -T option to curl is used to send the contents of the specified file as the 
    body of the request.  For more information see https://curl.haxx.se/docs/manual.html.


Response
""""""""""""""""

The operation returns an HTTP 204 Accepted response code, if successful. 
It does not return a response body.
