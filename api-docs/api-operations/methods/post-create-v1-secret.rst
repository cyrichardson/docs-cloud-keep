
.. _post-secret:

Create Secret
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /{version}/secrets

This method creates and stores a secret.

..  note::
    The POST request always creates and stores secret metadata. If a payload is provided with the POST request, it is encrypted and stored, and then linked with this metadata. If no payload is provided in the POST request, it must be provided in a subsequent PUT request.


The following table shows possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|201                       |Success                  |This status code is      |
|                          |                         |returned when the secret |
|                          |                         |has been successfully    |
|                          |                         |created.                 |
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned if the          |
|                          |                         |"payload" parameter is   |
|                          |                         |empty. This response     |
|                          |                         |indicates that the       |
|                          |                         |'payload' JSON attribute |
|                          |                         |was provided, but no     |
|                          |                         |value was assigned to it.|
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned if the secret   |
|                          |                         |has invalid data. This   |
|                          |                         |response may include     |
|                          |                         |schema violations such   |
|                          |                         |as mime-type not         |
|                          |                         |specified.               |
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |This error code is       |
|                          |                         |returned if the value    |
|                          |                         |specified in the         |
|                          |                         |"payload_content_type"   |
|                          |                         |parameter is not         |
|                          |                         |supported. It is caused  |
|                          |                         |when no crypto plugin    |
|                          |                         |supports the             |
|                          |                         |payload_content_type     |
|                          |                         |requested                |
+--------------------------+-------------------------+-------------------------+
|413                       |Error                    |This error code is       |
|                          |                         |returned when the secret |
|                          |                         |specified in the         |
|                          |                         |"payload" parameter is   |
|                          |                         |too large.               |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""


The following table shows the body parameters for the request:

+-----------------------------+---------------------+--------------------------+
|Name                         |Type                 |Description               |
+=============================+=====================+==========================+
|\ **name**                   |String *(Optional)*  |Specifies the human       |
|                             |                     |readable name for the     |
|                             |                     |secret. This parameter is |
|                             |                     |optional. If no name is   |
|                             |                     |supplied, the UUID will   |
|                             |                     |be displayed for this     |
|                             |                     |parameter on subsequent   |
|                             |                     |GET calls.                |
+-----------------------------+---------------------+--------------------------+
|\ **expiration**             |Integer *(Optional)* |Specifies the expiration  |
|                             |                     |date for the secret in    |
|                             |                     |ISO-8601 format. ISO-8601 |
|                             |                     |formats dates by using    |
|                             |                     |the following             |
|                             |                     |representation: yyyy-mm-  |
|                             |                     |ddThh:mm:ss[.mmm]. For    |
|                             |                     |example, September 27,    |
|                             |                     |2012 is represented as    |
|                             |                     |2012-09-27. Once the      |
|                             |                     |secret has expired, it is |
|                             |                     |no longer returned by the |
|                             |                     |API or agent. This        |
|                             |                     |parameter is optional. If |
|                             |                     |this parameter is not     |
|                             |                     |supplied, the secret has  |
|                             |                     |no expiration date.       |
+-----------------------------+---------------------+--------------------------+
|\ **algorithm**              |String *(Optional)*  |Specifies the algorithm   |
|                             |                     |type used to generate the |
|                             |                     |secret. This parameter is |
|                             |                     |optional. Barbican does   |
|                             |                     |not validate the          |
|                             |                     |information provided for  |
|                             |                     |this parameter because it |
|                             |                     |is client/application     |
|                             |                     |specific.                 |
+-----------------------------+---------------------+--------------------------+
|\ **bit_length**             |Integer *(Optional)* |Specifies the bit length  |
|                             |                     |of the secret. Must be a  |
|                             |                     |positive integer. This    |
|                             |                     |parameter is optional.    |
|                             |                     |Barbican does not         |
|                             |                     |validate the information  |
|                             |                     |provided for this         |
|                             |                     |parameter because it is   |
|                             |                     |client/application        |
|                             |                     |specific.                 |
+-----------------------------+---------------------+--------------------------+
|\ **mode**                   |String *(Optional)*  |Specifies the type/mode   |
|                             |                     |of the algorithm          |
|                             |                     |associated with the       |
|                             |                     |secret information. This  |
|                             |                     |parameter is optional.    |
|                             |                     |Barbican does not         |
|                             |                     |validate the information  |
|                             |                     |provided for this         |
|                             |                     |parameter because it is   |
|                             |                     |client/application        |
|                             |                     |specific.                 |
+-----------------------------+---------------------+--------------------------+
|\ **payload**                |String *(Optional)*  |Specifies the secret's    |
|                             |                     |unencrypted plain text.   |
|                             |                     |If this parameter is      |
|                             |                     |specified, the            |
|                             |                     |payload_content_type      |
|                             |                     |parameter must be         |
|                             |                     |specified as well. If     |
|                             |                     |this parameter is not     |
|                             |                     |specified, you can        |
|                             |                     |provide the payload       |
|                             |                     |information via a         |
|                             |                     |subsequent PUT request.   |
|                             |                     |If the payload is not     |
|                             |                     |provided, only the secret |
|                             |                     |metadata will be          |
|                             |                     |retrievable from Barbican |
|                             |                     |and any attempt to        |
|                             |                     |retrieve decrypted data   |
|                             |                     |for that secret will      |
|                             |                     |fail. Deferring the       |
|                             |                     |secret information to a   |
|                             |                     |PUT request is useful for |
|                             |                     |secrets that are in       |
|                             |                     |binary format and are not |
|                             |                     |suitable for base64       |
|                             |                     |encoding.                 |
+-----------------------------+---------------------+--------------------------+
|\ **payload_content_type**   |String *(Optional)*  |Specifies the type/format |
|                             |                     |the secret data is        |
|                             |                     |provided in. This         |
|                             |                     |parameter is required if  |
|                             |                     |the payload parameter is  |
|                             |                     |specified. The following  |
|                             |                     |values are supported: -   |
|                             |                     |"text/plain" - This value |
|                             |                     |is used to store plain    |
|                             |                     |text secrets. Other       |
|                             |                     |options are "text/plain;  |
|                             |                     |charset=utf-8". If the    |
|                             |                     |charset value is omitted, |
|                             |                     |UTF-8 will be assumed.    |
|                             |                     |Note that Barbican        |
|                             |                     |normalizes some formats   |
|                             |                     |before storing them as    |
|                             |                     |secret metadata, for      |
|                             |                     |example,"text/plain;      |
|                             |                     |charset=utf-8" is         |
|                             |                     |converted to              |
|                             |                     |"text/plain." Retrieved   |
|                             |                     |metadata may not exactly  |
|                             |                     |match what was originally |
|                             |                     |specified in the POST or  |
|                             |                     |PUT request. When the     |
|                             |                     |payload_content_type      |
|                             |                     |parameter is set to       |
|                             |                     |"text/plain" you cannot   |
|                             |                     |specify a value for the   |
|                             |                     |payload_content_encoding  |
|                             |                     |parameter. -              |
|                             |                     |"application/octet-       |
|                             |                     |stream" - This value is   |
|                             |                     |used to store binary      |
|                             |                     |secrets from a base64     |
|                             |                     |encoded payload. If this  |
|                             |                     |value is used, you must   |
|                             |                     |also include the          |
|                             |                     |payload_content_encoding  |
|                             |                     |parameter.                |
+-----------------------------+---------------------+--------------------------+
|\                            |String *(Optional)*  |Specifies the encoding    |
|**payload_content_encoding** |                     |format used to provide    |
|                             |                     |the payload data.         |
|                             |                     |Barbican may translate    |
|                             |                     |and store the secret data |
|                             |                     |into another format. This |
|                             |                     |parameter is required if  |
|                             |                     |the payload_content_type  |
|                             |                     |parameter is set to       |
|                             |                     |"application/octet-       |
|                             |                     |stream." The only         |
|                             |                     |supported value for this  |
|                             |                     |parameter is "base64,"    |
|                             |                     |which specifies base64-   |
|                             |                     |encoded payloads.         |
+-----------------------------+---------------------+--------------------------+


**Example:Create Secret: JSON request**


.. code::

   curl -X POST $ENDPOINT/v1/secrets -H 'Content-Type: application/json'\
   -H 'Accept: application/json -H 'X-Auth-Token: $AUTH-TOKEN' -d \
   '{
     "name": "key",
     "expiration": "2014-09-01T19:14:44.180394",
     "algorithm": "aes",
     "bit_length": 256,
     "mode": "cbc",
     "payload": "secretsecretsecret",
     "payload_content_type": "text/plain"
     }'

where:

- {endpoint} is the endpoint for the service
- $AUTH-TOKEN is the authentication token returned by the identity service

Response
""""""""""""""""

**Example:Create Secret: JSON response**


.. code::

   {
       "secret_ref": "https://iad.keep.api.rackspacecloud.com/v1/secrets/485950f0-37a5-4ba4-b1d6-413f79b849ef"
   }

where:

- the secret ID is 485950f0-37a5-4ba4-b1d6-413f79b849ef
- the endpoint is iad.keep.api.rackspacecloud.com
