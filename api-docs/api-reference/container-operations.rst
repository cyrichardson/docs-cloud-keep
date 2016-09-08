.. _container-api-operations:

==========
Containers
==========

A :ref:`container <containers-concept>` is a logical object that you can use
to store reference links to secrets resources that are related by relationship
or type. For example you can create a single container to group secrets for a
private key, certificate, and bundle for an SSL certificate.

You can use the following Containers API operations to create and manage
groups of related secrets for |product name| projects.

.. contents::
	 :local:
	 :depth: 1


.. include:: ../common-gs/env-variables-in-examples.rst
.. include:: methods/create-v1-container.rst
.. include:: methods/get-v1-containers.rst
.. include:: methods/get-v1-container-info.rst
.. include:: methods/delete-v1-container.rst
