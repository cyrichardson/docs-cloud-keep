.. _barbican-dg-rbac:

Role Based Access Control
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Like many other services, the |product name| service supports the protection of
its APIs by enforcing Role Based Access Control rules.  Sub-accounts can be
granted roles to allow or prevent access to secrets stored in |product name|

The account owner always has full access to all resources stored in |product name|,
while new sub-accounts will have no access by default.

The different roles that can be granted to sub-accounts will limit the amount
of access each sub-account has for all resources stored in |product name| as
listed in the following table:

.. csv-table::
   :header: "Role", "Read Metadata", "Retrieve Payloads", "Store new secrets", "Delete secrets"

   "keep:admin", "x", "x", "x", "x"
   "keep:creator", "x", "x", "x"
   "keep:observer or observer", "x", "x"
   "keep:audit", "x"

