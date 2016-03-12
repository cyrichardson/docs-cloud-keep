.. _container-api-operations:

Container API Operations
~~~~~~~~~~~~~~~~~~~~~~~~~~~

A :ref:`container <containers-concept>` is a logical object that can be used to store 
reference links to secrets resources that are related by relationship or type. 
For example you can create a single container to group  private key, certificate, 
and bundle for an SSL certificate. 

Use the Containers API operations to create and manage groups of related secrets for 
|product name| projects.


.. include:: ../common-gs/env_variables_in_examples.rst
.. include:: methods/post-create-v1-container.rst
.. include:: methods/get-get-v1-containers.rst
.. include:: methods/get-get-v1-container-info.rst
.. include:: methods/delete-delete-v1-container.rst
