# Устранение последствий переполнения хранилища кластера WAL-журналами


## Описание проблемы {#issue-description}

В работе кластера {{ mpg-name }} наблюдается одна или несколько указанных ниже проблем:

* В результате трансфера {{ data-transfer-name }} произошло переполнение хранилища данных базы;
* Превышено количество слотов репликации для кластера;
* Запись новых данных в таблицы в баз данных кластера не производится.

## Решение {#case-resolution}

Ошибки могут возникать из-за проблем со слотами репликации во время операций с базами кластера со стороны {{ data-transfer-name }}.

Каждый выполняющийся трансфер создает слот репликации в базе данных. Слот репликации – это указатель на позицию в WAL-журнале, если слот не используется, то позиция в журнале не изменяется.

Если данные из этого слота не читались по какой-то причине, размер WAL-журнала продолжает увеличиваться до тех пор, пока не закончится свободное место в хранилище кластера или пока не будет превышено значение [параметра `Max slot wal keep size`](../../../managed-postgresql/concepts/settings-list.md)

Узнать, какие слоты репликации открыты в базе можно, подключившись к одной из баз кластера с помощью `psql` и выполнив запрос `SELECT * FROM pg_replication_slots WHERE slot_type = 'logical';`.

{% cut "Пример вывода команды `SELECT * FROM pg_replication_slots WHERE slot_type = 'logical';`" %}

    ```sql
    SELECT * FROM pg_replication_slots WHERE slot_type = 'logical';
    -[ RECORD 1 ]-------+---------------------
    slot_name           | dttXXXXXXXXXXXXXXXXX
    plugin              | wal2json
    slot_type           | logical
    ```

{% endcut %}

* Если для поля `plugin` в слоте логической репликации указано значение `wal2json`, это означает, что с базами данных этого кластера в настоящий момент работает {{ data-transfer-name }};

* Если процессе работы трансфера для одного или нескольких слотов репликации ошибка, удалите его командой `SELECT pg_drop_replication_slot('$REPLICATION_SLOT_NAME');`, где `$REPLICATION_SLOT_NAME` – наименование залипшего порта репликации. Для  примера выше это `dttXXXXXXXXXXXXXXXXX`;

* Если в результате удаления слота репликации возникает ошибка `replication slot "$REPLICATION_SLOT_NAME" is active for PID $PID_NUM`, остановите выполнение трансфера на стороне {{ data-transfer-name }} или удалите из параметров трансфера задействованный эндпоинт.

{% cut "Пример вывода команды `select pg_drop_replication_slot('$REPLICATION_SLOT_NAME');`" %}

```sql
db-NAME=> SELECT pg_drop_replication_slot('$REPLICATION_SLOT_NAME');
ERROR: replication slot "$REPLICATION_SLOT_NAME" IS active FOR PID 12345
```
{% endcut %}

Также вы можете указать максимальный размер WAL-лога, после которого работа {{ data-transfer-name }} будет остановлена. Для этого измените значение [параметра `Max slot wal keep size`](../../../managed-postgresql/concepts/settings-list.md). Если размер WAL-журнала для вашей базы превысит размер, указанный в этом параметре, трансфер остановится. Это предотвратит заполнение всего свободного места в хранилище кластера.

После ошибки или успешного завершения трансфера WAL-журнал удаляется и пространство в хранилище высвобождается. В случае если трансфер не завершается успешно после изменения значения параметра  `Max slot wal keep size`, увеличьте размер хранилища кластера [по этой инструкции](../../../managed-postgresql/operations/update.md#change-disk-size).

Больше о работе слотов репликации вы можете узнать [из документации от разработчиков {{ PG }}](https://www.postgresql.org/docs/current/view-pg-replication-slots.html).