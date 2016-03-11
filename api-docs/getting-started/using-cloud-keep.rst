.. using-cloud-keep:

Create and manage secrets
---------------------------------------------- 

You can use the examples in this section to create and manage secrets 
by using |product name| API operations. Example requests are provided in
cURL, followed by the response.


Before running the examples, 
review the |product name| :ref:`concepts<concepts>` to understand the 
API workflow and use cases.  

.. note:: 
     These examples use the ``$ENDPOINT`` and ``$AUTH_TOKEN`` environment 
     variables to specify the API endpoint and authentication token  
     for accessing the service. Be sure to 
     :ref:`configure these variables<configure-environment-variables>` before running the 
     code samples. 


For more information about all Cloud Keep operations, see the
:ref:`API reference <api-reference>`.

.. include:: examples/store-a-secret.rst
.. include:: examples/retrieve-a-secret.rst
.. include:: examples/retrieve-list-of-secrets.rst
.. include:: examples/two-step-secret-creation.rst

