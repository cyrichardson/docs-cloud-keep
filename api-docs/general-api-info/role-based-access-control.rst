.. _barbican-dg-rbac:

Role Based Access Control
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Like many other services, the |product name| service supports the protection of
its APIs by enforcing policy rules defined in a policy file.  The |product name|
service stores a reference to a policy JSON file in its configuration file,
:file:`/etc/barbican/barbican.conf`.  Typically this file is named
``policy.json`` and it is stored in :file:`/etc/barbican/policy.json`.

Each |product name| API call has a line in the policy file that dictates which
level of access applies:

.. code-block:: ini

    API_NAME: RULE_STATEMENT or MATCH_STATEMENT

where ``RULE_STATEMENT`` can be another ``RULE_STATEMENT`` or a
``MATCH_STATEMENT``:

.. code-block:: ini

   RULE_STATEMENT: RULE_STATEMENT or MATCH_STATEMENT

``MATCH_STATEMENT`` is a set of identifiers that must match between the token
provided by the caller of the API and the parameters or target entities of the
API in question.  For example:

.. code-block:: ini

    "secrets:post": "role:admin or role:creator"

indicates that to create a new secret via a POST request, you must have either
the admin or creator role in your token.

.. warning:: The |product name| service scopes the ownership of a secret at
    the project level.  This means that many calls in the API will perform an
    additional check to ensure that the project_id of the token matches the
    project_id stored as the secret owner.

Default Policy
~~~~~~~~~~~~~~

The policy engine in OpenStack is very flexible and allows for customized
policies that make sense for your particular cloud.  The |product name| service
comes with a sample ``policy.json`` file which can be used as the starting
point for a customized policy.  The sample policy defines 5 distinct roles:

key-manager:service-admin
    The cloud administrator in charge of the |product name| service.  This user
    has access to all management APIs like the project quotas.

admin
    Project administrator.  This user has full access to all resources owned
    by the project for which the admin role is scoped.

creator
    Users with this role are allowed to create new resources but are not
    allowed to delete any existing resources.  They are also allowed full
    access to existing secrets owned by the project in scope.

observer
    Users with this role are allowed to access to existing resources but are
    not allowed to upload new secrets or delete existing secrets.

audit
    Users with this role are allowed access only to the resource metadata
    Users with this role are unable to decrypt secrets.
