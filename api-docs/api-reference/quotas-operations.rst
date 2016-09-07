.. _quotas-api-operations:

======
Quotas
======

:ref:`Quotas <quotas-concept>` to specify resource limits for a |product name|
project. |product name| provides a way to configure default quota values in the
Rackspace Cloud Keep configuration file (``barbican.conf``). The default values
are used unless a custom value is configured.

You can use the following Quotas API operations to retrieve a list of quotas
and to update or delete quota configurations for your project:

.. contents::
	 :local:
	 :depth: 1

.. include:: ../common-gs/env-variables-in-examples.rst
.. include:: methods/get-v1-project-quotas.rst
.. include:: methods/get-v1-project-quota-records.rst
.. include:: methods/get-v1-project-quota-details.rst
.. include:: methods/update-v1-configured-project-quotas.rst
.. include:: methods/delete-v1-project-quota-configuration.rst
