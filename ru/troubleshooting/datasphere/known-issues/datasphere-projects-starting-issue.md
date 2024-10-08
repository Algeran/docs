# Устранение ошибок при запуске проекта в {{ ml-platform-name }}


## Описание проблемы {#issue-description}

Не запускается проект в {{ ml-platform-full-name }}.

Возможные ошибки:

* Отображается сообщение `Веб страница по адресу yds.yandexcloud.net/tambour/folder-id/project-id временно недоступна` при открытии страницы проекта;
* Долго отображается индикатор загрузки проекта;
* Отображается сообщение `Ошибка 503`;
* Отображается сообщение `Deadline Exceeded`;
* При открытии кластера отображается пустая страница.
 
Проблема может наблюдаться со всеми проектами в {{ ml-platform-short-name }}.

{% note info %}

Загрузка масштабных проектов {{ ml-platform-short-name }} со множеством файлов может занимать до 10 минут. Если в вашем проекте включено много файлов и сторонних модулей – дождитесь их загрузки. 

Следить за сетевой активностью браузера в период загрузки проекта вы можете в инструментах разработчика браузера на вкладке **Network** (**Сеть**). Чтобы отобразить панель инструментов разработки на любой странице в браузере, нажмите `F12`.

{% endnote %}

## Решение {#issue-resolution}

При открытии проекта в IDE {{ ml-platform-short-name }} перенаправляет ваш запрос на внутренний хост с {{ jlab }}Lab. Современные браузеры могут блокировать такое поведение сайтов, если вы используете режимы повышенной конфиденциальности, в том числе режим инкогнито. 

Чтобы открыть проект в IDE, отключите блокирующие настройки:

* **Chrome**: разрешите использовать сторонние куки;
* **Safari**: отключите опцию **Отслеживание на веб-сайтах**. Для этого выберите **Предотвращать перекрестное отслеживание** в меню **Настройки** ⟶ **Конфиденциальность**;
* **Яндекс Браузер**: разрешите использование сторонних куки-файлов для {{ ml-platform-short-name }} в настройках браузера в разделе **Сайты** ⟶ **Расширенные настройки сайтов**.

Также проверьте [уровень текущего потребления]({{ link-console-quotas }}) в вашем облаке. Если квоты, используемые {{ ml-platform-short-name }}, превышены, это может привести к проблемам при запуске проектов.
