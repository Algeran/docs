# OS Login

OS Login — это удобный способ управления подключениями к [виртуальным машинам](../../compute/concepts/vm.md) и узлам [кластеров](../../managed-kubernetes/concepts/index.md#kubernetes-cluster) {{ managed-k8s-full-name }} по SSH c SSH-сертификатом через YC CLI или через стандартный SSH-клиент, а также через YC CLI с SSH-ключом, предварительно добавленным в профиль пользователя организации или [сервисного аккаунта](../../iam/concepts/users/service-accounts.md) в {{ org-full-name }}.

Агент OS Login разработан на основе [Guest Agent for Google Compute Engine](https://github.com/GoogleCloudPlatform/guest-agent). Изменения, внесенные командой {{ yandex-cloud }}, можно отслеживать в репозитории на [GitHub](https://github.com/yandex-cloud/yandex-cloud-guest-agent).

{% note info %}

Необходимые роли:

{% list tabs %}

- Подключение через YC CLI

  Для подключения через [YC CLI](../../cli/quickstart.md) к виртуальной машине или узлу {{ k8s }} с включенным доступом по OS Login пользователю или сервисному аккаунту, от имени которого выполняется команда YC CLI, должна быть назначена роль `compute.osLogin` или `compute.osAdminLogin`, а также роль `compute.operator`.

- Подключение через стандартный SSH-клиент

  Для подключения через стандартный SSH-клиент к виртуальной машине или узлу {{ k8s }} с включенным доступом по OS Login пользователю или сервисному аккаунту, от имени которого выполняется подключение, должна быть назначена роль `compute.osLogin` или `compute.osAdminLogin`.

{% endlist %}

{% endnote %}

OS Login связывает учетную запись пользователя виртуальной машины или узла {{ k8s }} с учетной записью пользователя организации. Для управления доступом к виртуальным машинам и узлам [включите на уровне организации опцию](../operations/os-login-access.md), разрешающую доступ по OS Login, а затем активируйте ее отдельно на каждой виртуальной машине или узле {{ k8s }}.

Так можно легко управлять доступом к виртуальным машинам и узлам {{ k8s }}, назначая пользователю необходимые роли. Если у пользователя отозвать роли, он потеряет доступ ко всем виртуальным машинам и узлам {{ k8s }}, для которых включен доступ по OS Login.

Пользователи или сторонние инструменты, такие как [{{ TF }}](https://www.terraform.io/) или [Ansible](https://www.ansible.com/), могут использовать стандартный SSH-клиент, чтобы [подключаться](../../compute/operations/vm-connect/os-login.md#connect-via-exported-certificate) к ВМ и узлам {{ k8s }} с включенным доступом по OS Login с помощью SSH-сертификатов или SSH-ключей.

Чтобы подключиться через стандартный SSH-клиент с использованием SSH-сертификата к ВМ или узлу {{ k8s }} с включенным доступом по OS Login, нужно [экспортировать](../../compute/operations/vm-connect/os-login-export-certificate.md) сертификат OS Login и использовать его при подключении. Сертификат действителен один час. По истечении этого времени для подключения к ВМ или узлу {{ k8s }} необходимо экспортировать новый сертификат.

Чтобы [подключиться](../../compute/operations/vm-connect/os-login.md#connect-via-key) к ВМ или узлу {{ k8s }} с включенным доступом по OS Login через YC CLI с SSH-ключом, нужно [создать SSH-ключ](../../compute/operations/vm-connect/ssh.md#creating-ssh-keys) и [добавить](../../organization/operations/add-ssh.md) его в профиль пользователя организации в {{ org-name }}. Вы также можете добавить SSH-ключ в профиль [сервисного аккаунта](../../iam/concepts/users/service-accounts.md), чтобы иметь возможность [подключаться](../tutorials/sa-oslogin-ansible.md) к ВМ по OS Login от имени этого сервисного аккаунта. 

Преимущества OS Login:

* моментальное обновление прав доступа в случае отзыва или назначения ролей;
* возможность доступа по короткоживущим SSH-сертификатам;
* возможность доступа по SSH-ключам;
* возможность восстановления доступа к ВМ и узлам кластеров {{ k8s }} в случае утери SSH-ключей (если используются обычные SSH-ключи, а не OS Login);
* возможность загрузки пользователем собственных SSH-ключей в свой профиль.

#### Что дальше {#what-is-next}

* [{#T}](../operations/os-login-access.md)
* [{#T}](../operations/os-login-profile-create.md)
* [{#T}](../../compute/operations/vm-connect/os-login.md)
* [Подключиться к узлу {{ k8s }} через OS Login](../../managed-kubernetes/operations/node-connect-oslogin.md)
* [Использовать сервисный аккаунт с профилем OS Login для управления ВМ с помощью Ansible](../tutorials/sa-oslogin-ansible.md)