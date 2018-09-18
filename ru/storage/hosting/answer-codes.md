# Коды ответов

Если корзина сконфигурирована для хостинга статических сайтов, то при обращении к ней пользователь может получить ошибки, описанные в таблице ниже.

Код ошибки | Описание
-----------|---------
`200 OK` | Успешный ответ.
`302 Found`  | Если в [!KEYREF objstorage-name] поступил запрос к ресурсу `http:/website.cloud.yandex.net/bucket/x` без конечного `/`, то сначала [!KEYREF objstorage-name] попытается найти объект `x` и, если объекта не существует, но существует `x/index.html`, который установлен как главная страница сайта, то пользователь получит ответ с кодом 302 и редиректом к ресурсу `http:/website.cloud.yandex.net/bucket/x/`.
`304 Not Modified` | [!KEYREF objstorage-name] использует заголовки запроса `If-Modified-Since`, `If-Unmodified-Since`, `If-Match`, `If-None-Match` чтобы определить изменился ли объект по отношению к ранее закэшированному на стороне клиента. Если объект не изменился, то пользователь получит ответ `304 Not Modified`.
`403 Forbidden` | Возвращается, если для корзины, к которой направлен запрос, не настроен публичный доступ.<br/><br/>[[!TITLE ../operations/security/bucket-availability.md]](../operations/security/bucket-availability.md).
`404 Not Found` | Возвращается, если ресурс, к которому направлен запрос не существует, или корзина, в которой находится запрошенный ресурс не сконфигурирована для хостинга статических сайтов.<br/><br/>[Конфигурирование корзины для хостинга статических сайтов](bucket-configuration.md).
`500 Service Error` | Внутренняя ошибка [!KEYREF objstorage-name].
`503 Service Unavailable` | Слишком высокая нагрузка на сервис. Необходимо снизить частоту запросов.