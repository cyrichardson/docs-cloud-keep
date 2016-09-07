.. _service-access:

========================
Service access endpoints
========================

The |apiservice| is a regionalized service. The user of the service is
therefore responsible for selecting the appropriate regional endpoint to
ensure access to servers, networks, or other Cloud services.

.. tip::
   To help you decide which regionalized endpoint to use, read about
   special considerations for choosing a data center at
   :how-to:`About regions <about-regions>`.

If you are working with cloud services that are in one of the Rackspace
data centers, using the ``ServiceNet`` endpoint in the same data center has
no network costs and provides a faster connection. ``ServiceNet`` is the
data center internet network. In your authentication response service
catalog, it is listed as ``InternalURL``.

If you are working with servers that are not in one of the Rackspace data
centers, you must use a public endpoint to connect. In your authentication
response, public endpoints are listed as ``publicURL``. If you are working with
servers in multiple data centers or have a mixed environment where you have
servers in your data centers and in Rackspace data centers, use a public
endpoint because it is accessible from all the servers in the different
environments.

.. tip::
   If you do not know your account ID or which data center you are
   working in, you can find that information in your Cloud Control Panel at
   `mycloud.rackspace.com. <http://mycloud.rackspace.com>`__

.. list-table:: **Regionalized service endpoints**
   :widths: 10 40
   :header-rows: 1

   * - Region
     - Endpoint
   * - Chicago (ORD)
     - ``https://ord.keep.api.rackspacecloud.com/v1/``
   * - Dallas (IAD)
     - ``https://iad.keep.api.rackspacecloud.com/v1/``
   * - London (LON)
     - ``https://lon.keep.api.rackspacecloud.com/v2/``
