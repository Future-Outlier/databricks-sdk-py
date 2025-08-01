``w.account_access_control_proxy``: Account Access Control Proxy
================================================================
.. currentmodule:: databricks.sdk.service.iam

.. py:class:: AccountAccessControlProxyAPI

    These APIs manage access rules on resources in an account. Currently, only grant rules are supported. A
    grant rule specifies a role assigned to a set of principals. A list of rules attached to a resource is
    called a rule set. A workspace must belong to an account for these APIs to work

    .. py:method:: get_assignable_roles_for_resource(resource: str) -> GetAssignableRolesForResourceResponse

        Gets all the roles that can be granted on an account level resource. A role is grantable if the rule
        set on the resource can contain an access rule of the role.

        :param resource: str
          The resource name for which assignable roles will be listed.

          Examples | Summary :--- | :--- `resource=accounts/<ACCOUNT_ID>` | A resource name for the account.
          `resource=accounts/<ACCOUNT_ID>/groups/<GROUP_ID>` | A resource name for the group.
          `resource=accounts/<ACCOUNT_ID>/servicePrincipals/<SP_ID>` | A resource name for the service
          principal.

        :returns: :class:`GetAssignableRolesForResourceResponse`
        

    .. py:method:: get_rule_set(name: str, etag: str) -> RuleSetResponse

        Get a rule set by its name. A rule set is always attached to a resource and contains a list of access
        rules on the said resource. Currently only a default rule set for each resource is supported.

        :param name: str
          The ruleset name associated with the request.

          Examples | Summary :--- | :--- `name=accounts/<ACCOUNT_ID>/ruleSets/default` | A name for a rule set
          on the account. `name=accounts/<ACCOUNT_ID>/groups/<GROUP_ID>/ruleSets/default` | A name for a rule
          set on the group.
          `name=accounts/<ACCOUNT_ID>/servicePrincipals/<SERVICE_PRINCIPAL_APPLICATION_ID>/ruleSets/default` |
          A name for a rule set on the service principal.
        :param etag: str
          Etag used for versioning. The response is at least as fresh as the eTag provided. Etag is used for
          optimistic concurrency control as a way to help prevent simultaneous updates of a rule set from
          overwriting each other. It is strongly suggested that systems make use of the etag in the read ->
          modify -> write pattern to perform rule set updates in order to avoid race conditions that is get an
          etag from a GET rule set request, and pass it with the PUT update request to identify the rule set
          version you are updating.

          Examples | Summary :--- | :--- `etag=` | An empty etag can only be used in GET to indicate no
          freshness requirements. `etag=RENUAAABhSweA4NvVmmUYdiU717H3Tgy0UJdor3gE4a+mq/oj9NjAf8ZsQ==` | An
          etag encoded a specific version of the rule set to get or to be updated.

        :returns: :class:`RuleSetResponse`
        

    .. py:method:: update_rule_set(name: str, rule_set: RuleSetUpdateRequest) -> RuleSetResponse

        Replace the rules of a rule set. First, use get to read the current version of the rule set before
        modifying it. This pattern helps prevent conflicts between concurrent updates.

        :param name: str
          Name of the rule set.
        :param rule_set: :class:`RuleSetUpdateRequest`

        :returns: :class:`RuleSetResponse`
        