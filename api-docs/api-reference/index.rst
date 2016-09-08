.. _api-reference:

=============
API Reference
=============

Learn about the available |apiservice| resources and operations, and see
request and response examples. You can use the |apiservice| operations to
interact directly with the service.

..  note::

    This document refers to version "v1" of the API. When you submit a request
    to the |apiservice|, append the version number to the API endpoint in the
    URI, for example
    ``$ENDPOINT/v1/containers/{containerID}/consumers``. In the examples, replace any
    *{version}* place holder values with ``v1``.

|apiservice| provides the following resources for managing keys and
credentials.

.. toctree::
   :maxdepth: 1

   secrets-operations
   container-operations
   consumers-operations
   quotas-operations
