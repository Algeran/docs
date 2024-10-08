Подключиться к виртуальной машине с включенным доступом по OS Login можно с помощью пользовательского [SSH-ключа](../../glossary/ssh-keygen.md). Для этого [создайте](../../compute/operations/vm-connect/ssh.md#creating-ssh-keys) SSH-ключ, [добавьте](../../organization/operations/add-ssh.md) его в профиль пользователя организации или сервисного аккаунта в {{ org-full-name }} и укажите при подключении:

1. [Включите](../../organization/operations/os-login-access.md) доступ по OS Login на уровне организации.

    Чтобы подключиться к ВМ по OS Login с SSH-ключом через YC CLI, включите опцию **{{ ui-key.yacloud_org.form.oslogin-settings.title_user-ssh-key-settings }}**.

1. Получите список всех ВМ в каталоге по умолчанию:

    ```bash
    yc compute instance list
    ```

    Результат:

    ```text
    +----------------------+-----------------+---------------+---------+---------------+--------------+
    |          ID          |       NAME      |    ZONE ID    | STATUS  |  EXTERNAL IP  | INTERNAL IP  |
    +----------------------+-----------------+---------------+---------+---------------+--------------+
    | fhm0b28lgf********** | first-instance  | {{ region-id }}-a | RUNNING | 158.160.**.** | 192.168.0.8  |
    | fhm9gk85nj********** | second-instance | {{ region-id }}-a | RUNNING | 51.250.**.*** | 192.168.0.12 |
    +----------------------+-----------------+---------------+---------+---------------+--------------+
    ```

1. Подключитесь к ВМ:

    ```bash
    yc compute ssh \
      --name <имя_ВМ> \
      --identity-file <путь_к_файлу_закрытого_SSH_ключа> \
      --login <имя_пользователя> \
      --internal-address
    ```

    Где:

    * `--name` — полученное ранее имя виртуальной машины. Вместо имени ВМ можно указать ее идентификатор, для этого используйте параметр `--id`.
    * `--identity-file` — путь к сохраненному ранее файлу закрытого SSH-ключа. Например: `/home/user1/.ssh/id_ed25519`. 
    * `--login` — имя пользователя в профиле OS Login.
    * (опционально) `--internal-address` — для подключения по внутреннему IP-адресу.

Произойдет подключение к указанной виртуальной машине с помощью SSH-ключа. Если это ваше первое подключение, в операционной системе ВМ будет создан новый профиль пользователя.