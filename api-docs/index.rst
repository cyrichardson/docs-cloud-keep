.. _index:

=====================================
|product name| API |contract version|
=====================================

*Last updated:* |today|

|product name| is a key management service backed by a Hardware Security Module
(HSM) to provide FIPS certified secret storage, encryption, and decryption of
keys and credentials. The product enables secure life-cycle management of keys
and credentials, called *secrets*, on behalf of customers. |product name|
is based on the OpenStack Key Manager service (code named Barbican), a
community-led open-source platform.

.. note::

   |product name| is available on a limited availability basis until March
   2017. For details, see
   :ref:`Limited Availability Program <limited-availability-program>`.

Interactions with |product name| occur programmatically via a REST API. Using
the API, you can securely store and retrieve credentials systematically using
the following resources:

-  Secrets

-  Containers

-  Quotas

-  Consumers

This guide is intended to assist software developers who want to develop
applications by using the REST application programming interface (API) for
the |product name| service.

To use the information provided here, you should have a general understanding
of the service and have access to an installation of it. You should also be
familiar with the following technologies:

*  RESTful web services
*  HTTP/1.1
*  JSON data serialization format


Use the following links to go directly to user and reference information for
using the |apiservice|:

- :ref:`Getting started <getting-started-guide>`
- :ref:`General API information <general-api-info>`
- :ref:`API reference <api-reference>`
- :ref:`Release notes <release-notes-collection>`

.. toctree:: :hidden:
   :maxdepth: 2

   Cloud Keep v1.0 <self>
   limited-availability
   getting-started/index
   general-api-info/index
   api-reference/index
   release-notes/index
   service-updates
   additional-resources
   copyright
