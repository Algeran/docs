# Как восстановить удаленные данные из бакета


## Описание сценария {#case-description}

Необходимо восстановить данные, случайно удаленные из бакета {{ objstorage-name }}.

## Решение {#case-resolution}

Проверьте, было ли включено версионирование в свойствах бакета. Восстановить данные получится, если оно было включено.

## Если ничего не получилось {#if-nothing-worked}

Если вышеописанные действия не помогли решить задачу, [создайте запрос в техническую поддержку]({{ link-console-support }}). При создании запроса укажите следующую информацию:

1. Имя бакета.
1. Примерные дату и время удаления объектов.
1. Имена объектов либо ссылки на них.

{% note warning %}

Техническая поддержка не дает гарантий восстановления данных, самостоятельно удаленных пользователями из бакетов {{ objstorage-name }}. Во время работы специалистов технической поддержки над обращением рекомендуем ничего не записывать в затронутый бакет.

{% endnote %}