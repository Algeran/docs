# Устранение ошибки `ERR.DS_API.REQUEST_TIMEOUT`


## Описание проблемы {#issue-description}

Построение чарта завершается ошибкой `ERR.DS_API.REQUEST_TIMEOUT` после длительного ожидания.

## Решение {#issue-resolution}

Повысить порог времени ожидания данных на стороне {{ datalens-name }} не получится. Рекомендуем разбить наиболее затратные задачи на части или использовать фильтрацию данных для уменьшения их количества.

## Если проблема осталась {#if-issue-still-persists}

Если вышеописанные действия не помогли решить проблему, [создайте запрос в техническую поддержку]({{ link-console-support }}). При создании запроса укажите следующую информацию:

1. Ссылку на проблемный объект в {{ datalens-name }}: чарт или дашборд.
1. `Request ID` проблемного запроса — он отображается на странице с ошибкой.