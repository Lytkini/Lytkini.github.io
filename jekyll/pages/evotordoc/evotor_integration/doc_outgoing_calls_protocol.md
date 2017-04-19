---
title: Запросы к стороннему сервису
keywords: sample
summary: "Раздел содержит информацию о запросах Эвотора к стороннему сервису."
sidebar: evotordoc_sidebar
permalink: doc_outgoing_calls_protocol.html
folder: evotordoc/evotor_integration
---

## Запросы к стороннему сервису

В зависимости от функциональности стороннего сервиса, его REST API должен поддерживать соответствующие [запросы от облака Эвотор](https://api.evotor.ru/docs/#!/Inventory/post_api_v1_inventories_stores_storeUuid_products_delete).
Схема взаимодействия стороннего сервиса с платформой выглядит следующим образом:

![схема взаимодействия](ссылка на схему)

### Авторизация
В зависимости от способа авторизации в стороннем сервисе, запросы облака Эвотор могут содержать заголовок `Authorization` с типом `Basic` или `Bearer`:

* Для авторизации с типом `Basic`, в Эвотор требуется предоставить имя пользователя и пароль.

* Для авторизации с типом `Bearer`,  в Эвотор требуется предоставить ключ авторизации в формате `string`.

После запросов `/create`, `/verify`, `/tariff`, сторонний сервис сообщает облаку Эвотор *пользовательский ключ авторизации*, который облако передаёт в заголовках `Authorization` с типом `Bearer`.

Сторонний веб-сервис также может обращаться в облако Эвотор за дополнительной информацией. Ключ для авторизации таких запросов, облако Эвотор отправляет на адрес `http://<веб-адрес стороннего сервиса>/api/v1/user/token`. Подробнее, см. раздел **Авторизация** на странице [REST API облака Эвотор](https://dev.evotor.r1nat.com/evotor-cloud-rest-api/).

### Пример POST-запроса
Проверить данные учётной записи.
Запрос:
```curl
-X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Basic RXhhbXBsZXBhc3N3b3Jk' -d '{"userUuid":"01-000000000000001","username":"<Имя учётной записи>","password":"<пароль учётной записи>","customField":"любое значение"}' 'https://partner.org/api/v1/user/verify'
```

Ответ:

```JSON
{
  "userUuid": "01-000000000000001",
  "hasBilling": false,
  "token": "пользовательский токен"
}
```

### Пример PUT-запроса
Передать список магазинов в сторонний сервис.
Запрос:

```curl
-X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: <пользовательсский токен>' -d '[{"uuid": "string", "name": "string", "address": "string"}]' 'https://partner.org/api/v1/inventories/stores'
```

Ответ:

```JSON
[
  {
    "uuid": "string",
    "parentId": "string",
  }
]
```
### Справочник API
Ознакомиться и испробовать запросы к REST API облака Эвотор вы можете на сайте https://api.evotor.ru/docs в разделе **Протокол исходящих запросов**.
