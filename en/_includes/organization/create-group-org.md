{% list tabs group=instructions %}

- {{ org-name }} interface {#cloud-org}

  1. [Log in]({{ link-passport-login }}) as the organization administrator.
  1. Go to [{{ org-full-name }}]({{ link-org-main }}).
  1. In the left-hand panel, select **{{ ui-key.yacloud_org.pages.groups }}** ![icon-services](../../_assets/console-icons/persons.svg).
  1. In the top-right corner, click **{{ ui-key.yacloud_org.entity.group.action_create }}** and enter a [group](../../organization/concepts/groups.md) name and description.

      The name must be unique within the organization and satisfy the relevant requirements:

      {% include [group-name-format](group-name-format.md) %}

- {{ TF }} {#tf}

  {% include [terraform-definition](../../_tutorials/_tutorials_includes/terraform-definition.md) %}

  {% include [terraform-install](../../_includes/terraform-install.md) %}

  1. In the configuration file, describe the [group](../../organization/concepts/groups.md) parameters:

     ```hcl
     resource "yandex_organizationmanager_group" "my-group" {
        name            = "<group_name>"
        description     = "<group_description>"
        organization_id = "<organization_ID>"
     }
     ```

     Where:
     * `name`: Group name. The name must be unique within the organization and satisfy the relevant requirements:

        {% include [group-name-format](group-name-format.md) %}

     * `description`: Group description. This is an optional parameter.
     * `organization_id`: ID of the organization to add the group to.
  1. Create resources:

     {% include [terraform-validate-plan-apply](../../_tutorials/_tutorials_includes/terraform-validate-plan-apply.md) %}

     {{ TF }} will create all the required resources. You can check the new resources and their configuration using the [management console]({{ link-console-main }}) or this [CLI](../../cli/) command:

     ```bash
     yc organization-manager group list --organization-id=<organization_ID>
     ```

{% endlist %}
