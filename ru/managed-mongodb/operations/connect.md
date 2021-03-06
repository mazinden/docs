# Подключение к базе данных в кластере {{ MG }}

К хостам кластера {{ mmg-short-name }} можно подключиться:

{% include [cluster-connect-note](../../_includes/mdb/cluster-connect-note.md) %}

Для подключения к хостам кластеров {{ mmg-name }} указывайте порт 27018.

{% note info %}

Если публичный доступ в вашем кластере настроен только для некоторых хостов, автоматическая смена основной реплики может привести к тому, что вы не сможете подключиться к основной реплике из интернета.

{% endnote %}

## Ограничения на количество подключений {#connection-limits}

Максимальное доступное количество одновременных подключений к отдельному хосту кластера {{ mmg-name }} зависит от объема оперативной памяти этого хоста:

| Объем оперативной памяти | Максимальное количество подключений |
| ------------------------ | ------------------------------------|
| 2 ГБ | 2048 |
| 4 ГБ | 4096 |
| 8 ГБ | 8192 |
| 16 ГБ и выше | 16384 |

Доступный хосту объем оперативной памяти определяется классом этого хоста. Все доступные варианты перечислены в разделе [{#T}](../concepts/instance-types.md). 

## Настройка SSL-сертификата {#configuring-an-ssl-certificate}

{{ MG }}-хосты с публичным доступом поддерживают только соединения с SSL-сертификатом. Подготовить сертификат можно так:


```bash
mkdir ~/.mongodb && \
wget "https://storage.yandexcloud.net/cloud-certs/CA.pem" -O ~/.mongodb/root.crt && \
chmod 0600 ~/.mongodb/root.crt
```


## Примеры строк подключения {#connection-string}

{% include [conn-strings-environment](../../_includes/mdb/mdb-conn-strings-env.md) %}

Вы можете подключаться к {{ MG }}-хостам в публичном доступе только с использованием SSL-сертификата. Перед подключением к таким хостам [подготовьте сертификат](#configuring-an-ssl-certificate).

В этих примерах предполагается, что SSL-сертификат `root.crt` расположен в директории `/home/<домашняя директория>/.mongodb/`. 

Подключение без использования SSL-сертификата поддерживается только для хостов, находящихся не в публичном доступе. В этом случае трафик внутри виртуальной сети при подключении к БД шифроваться не будет.

Запросы на запись будут автоматически направлены к основной реплике кластера.

{% include [see-fqdn-in-console](../../_includes/mdb/see-fqdn-in-console.md) %}

{% include [mmg-connection-strings](../../_includes/mdb/mmg-conn-strings.md) %}

При успешном подключении к кластеру и выполнении тестового запроса будут выведены:
1. Для примеров на PHP — результат выполнения команды `ping`.
1. Для других примеров — имя БД, к которой было выполнено подключение.


