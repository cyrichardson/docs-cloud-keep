.. _barbican-dg-common-headers:

Common headers
^^^^^^^^^^^^^^^^

The following table describes the common headers used by the API.

**Table: Common headers**

+-----------------------+----------------------------------------------------+
| Header                | Description                                        |
+=======================+====================================================+
| X-Auth-Token          | Used to provide the authentication token issued by |
|                       | the Rackspace Identity System.  It is required for |
|                       | all requests sent to the Cloud Keep system.        |
+-----------------------+----------------------------------------------------+
| Accept                | Used to specify the media type preferred for the   |
|                       | response.  When not provided, the service uses a   |
|                       | suitable default.                                  |
+-----------------------+----------------------------------------------------+
| Content-Type          | Used to describe the media type of the request     |
|                       | body.                                              |
+-----------------------+----------------------------------------------------+
