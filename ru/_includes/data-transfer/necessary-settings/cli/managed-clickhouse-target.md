* {% include [Field CLI Cluster ID](../../fields/common/cli/cluster-id.md) %}
* `--cluster-name` — группа шардов, в которую будут передаваться данные. Если параметр не указан, данные будут размещены во всех шардах.
* {% include [Field CLI Database](../../fields/common/cli/database.md) %}
* {% include [Field CLI User](../../fields/common/cli/username.md) %}
* {% include [Field CLI Security Group](../../fields/common/cli/security-group.md) %}

    Убедитесь, что указанные группы безопасности [настроены](../../../../managed-clickhouse/operations/connect/index.md#configuring-security-groups).


* Чтобы задать пароль пользователя для доступа к базе данных, используйте один из параметров:

    * {% include [Field CLI Raw Password](../../fields/common/cli/raw-password.md) %}
    * {% include [Field CLI Password File](../../fields/common/cli/password-file.md) %}
