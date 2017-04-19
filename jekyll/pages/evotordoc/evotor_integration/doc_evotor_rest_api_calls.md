---
title: Запросы REST API Эвотор
keywords: sample
summary: "Раздел содержит информацию о запросах, которые вы можете отправлять в REST API Эвотор"
sidebar: evotordoc_sidebar
permalink: doc_evotor_rest_api_calls.html
folder: evotordoc/evotor_integration
---

Для доступа к данным пользователей платформы, вы можете обращаться к REST API облака Эвотор. Интеграция с REST API облака позволяет:
* искать магазины, сотрудников и смарт терминалы пользователя платформы (владельца бизнеса);
* получать и передавать информацию о продуктах в рамках выбранного магазина (*отдельного магазина пользователя*);
* удалять продукты в рамках выбранного магазина (*отдельного магазина пользователя*);
* получать документы в рамках выбранного магазина (*отдельного магазина пользователя*).

Схема взаимодействия приложений и облака Эвотор выглядит следующим образом:

![схема взаимодействия](ссылка на схему)

Актуальный список запросов, которые поддерживает облако Эвотор, вы найдёте на странице https://api.evotor.ru/docs.

### Авторизация
Все запросы к REST API облака Эвотор, должны содержать HTTP-заголовок `x-Authorization`, в котором требуется указать *ключ авторизации*. Ключ авторизации можно получить одним из следующих способов:
* В GET-параметре `token` веб-адреса iframe-приложения:
```curl
https://partner.org/#/?uid=01-000000000011111&token=string
```
* В Личном кабинете пользователя Эвотор, в разделе **Настройки** приложения.

![Токен для интеграции с 1с](https://github.com/Lytkini/Drafts/blob/Content-modification/pictures/1c_integration_API_key.png)

* В POST-запросе от облака Эвотор. Для этого сторонний сервис должен поддерживать адрес `http://<веб-адрес стороннего сервиса>/api/v1/user/token`.

### Пример GET-запроса к облаку Эвотор
Получить список всех магазинов пользователя:
```curl
-X GET --header 'Accept: application/json' --header 'X-Authorization: <ключ авторизации>' --header 'Content-Type: application/json' 'https://api.evotor.ru/api/v1/inventories/stores/search'
```
Ответ:
```JSON
[
  {
    "uuid": "string",
    "address": null,
    "name": "Мой магазин1",
    "code": null
  },
  {
    "uuid": "string",
    "address": null,
    "name": "Мой магазин3",
    "code": null
  }
]
```
### Пример POST-запроса
Создать новый товар в определённом магазине:
```curl
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'X-Authorization: <токен>' -d '[{"uuid":"n1e2w3-t4ov5qr6","code":"","barCodes":[],"alcoCodes":[],"name":"Новый товар","price":0,"quantity":0,"costPrice":0,"measureName":"","tax":"NO_VAT","allowToSell":false,"description":"","articleNumber":"","parentUuid":"","group":false,"type":"NORMAL","alcoholByVolume":0,"alcoholProductKindCode":0,"tareVolume":0}]' 'https://api.evotor.ru/api/v1/inventories/stores/storeUuid-123456/products'
```

```curl
no cotent
```

При создании товаров в ответ приходит пустое сообщение. Код ответа в случае удачного добавления -- 200.

### Справочник API
Ознакомиться и попробовать запросы к REST API облака Эвотор вы можете на сайте https://api.evotor.ru/docs в разделе **REST API облака Эвотор**.
