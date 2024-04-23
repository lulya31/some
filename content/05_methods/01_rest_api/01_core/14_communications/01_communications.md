---
title: "Коммуникации (communications)"
description: "Создание коммуникации"
version: 1
additional:
    team: ""
    author: ""
    service : "Communications"
    maintainer: ""
    developer: ""
    status: "in_work"
    subscribers: [""]
draft: false
weight: 1
---

{{<notice info>}}

[Описание переходов статусов, JSON представление сущности и атрибутивный состав](https://doc-communications-main.com-dev.int.rolfcorp.ru/02_info_model/02_entities/01_communication/)

{{</notice>}}


## Типы Коммуникации
Коммуникацией является любой из перечисленных типов взаимодействия:
* Звонок
* Визит
* СМС
* Заявка на сайте
* Электронная почта
* Заявка в мобильном приложении
* Обычная почта ( пока не планируется реализовывать )
* Мессенджер
* ЭДО ( пока не планируется реализовывать )

## Признаки коммуникации
* Фактическая - взаимодействие в реальном времени.
* Запланированная - взаимодействие, которое будет происходить в соответствии с заранее определенным планом или графиком.
состоявшееся?

## Виды коммуникации
* Входящая - коммуникация, при которой сотрудник получает запрос из вне.
* Исходящая - коммуникация, при которой сотрудник отправляет запрос.



## СТАТУСЫ КОММУНИКАЦИИ
1. Создана
2. В работе ( например, фактическая коммуникация =клиент находится в салоне, продолжается разговор по телефону и т.д. )
4. Выполнена ( Поговорили с клиентом, клиент ушел из салона и т.д. `date_finish is not null`)
5. Отменена ( отменена сотрудником. Например, не стали звонить `is_cancelled = true` )
6. Аут ( не состоялась, но пытались. Например, звонили несколько раз `is_failed = true` )

**Для ФАКТИЧЕСКОЙ:**
1. В работе
2. Выполнена 
3. Аут (если надо зафиксировать факт недозвона)

**Для ЗАПЛАНИРОВАННОЙ:**
1. Создана
2. В работе
3. Выполнена 
4. Отменена
5. Аут 


## Основные свойства


## Информационная модель

```json

```




## Методы

| Тип метода | URL                                      | Бизнес-домен | Описание                                                                                                                                        |
| :--------: | :--------------------------------------- | :----------: | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| GET        | [/v2/communications/{uuid}](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/14_get_communication/)                                  | CORE         | Дефиниция для получения полной или короткой инфо-модели по входному UUID и query-параметрам                                                                                                                              |
| POST       | [/v3/collections/communications](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/15_get_communication_info_models_v3/)                   | CORE         | Дефиниция для сбора коллекции инфо-моделей коммуникаций                                                                                                                                    |
| GET        | [/v3/communications](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/12_get_communications/)                                 | CORE         | Дефиниция для получения выборки из коллекции коммуникаций в соответствии с входными параметрами                                                                                                                                     |
| GET        | [/v2/communications/{uuid}/primary-info](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/03_get_communication_primary_info/)   | CORE         | Дефиниция необходима для отображения информации на фронте                                                                                                                                          |
| GET        | [/v2/dicts/communications-methods](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/05_get_dicts_communications_methods/)                   | CORE         | Дефиниция необходима для получения списка возможных методов коммуникаций (словарь)                                                                                                                                       |
| GET        | [/v1/communications/id-translations](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/10_get_communication_id_translation/)                   | CORE         | Дефиниция необходима для получения связи уникальных идентификаторов коммуникации между Flora и Oracle                                                                                                               |
| POST       | [/v1/communications/id-translations](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/09_create_communication_id_translation/)                | CORE         | Дефиниция необходима для создания связи уникальных идентификаторов коммуникации между Flora и Oracle                                                                                                                                          |
| POST       | [/v2/communications](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/07_create_communication/)                               | CORE         | Дефиниция предназначена для создания коммуникации                                                                                                                                    |
| POST       | [/v2/communications/{uuid}/call-phone](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/08_communication_call_phone/)         | CORE         | Дефиниция необходима для осуществления звонка через Asterisk из коммуникации                                                                                                                                    |
| PATCH      | [/v2/communications/{uuid}](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/04_update_communication/)                               | CORE         | Дефиниция для обновления данных коммуникации                                                                                                                                    |
| PATCH      | [/v2/communications/{uuid}/close](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/06_update_communication_to_closed/)                     | CORE         | Дефиниция необходима для закрытия активной коммуникации                                                                                                                                    |
| PATCH      | [/v2/communications/{uuid}/failed](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/13_update_communication_to_failed/)                     | CORE         | Дефиниция необходима для отметки коммуникации как несостоявшейся                                                                                                                                  |
| POST       | [/v2/communications/{uuid}/cancel](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/16_update_communication_to_cancelled/)                  | CORE         | Дефиниция необходима для отмены запланированной коммуникации                                                                                                                                    |
| DELETE     | [/v2/communications/{uuid}](https://doc-communications-main.com-dev.int.rolfcorp.ru/03_methods/01_rest/01_communications/11_delete_communication/)                               | CORE         | Дефиниция необходима для удаления коммуникации                                                                                                                                    |


### Примеры использования



### Требуется для разработки

| #   | Метод | Endpoint | Description | Priority | Comments |
| --- | ----- | -------- | ----------- | -------- | -------- |
|     |       |          |             |          |          |
|     |       |          |             |          |          |
|     |       |          |             |          |          |


### Доработки

| #   | Текущий | Новый | Задача | Comments |
| --- | ------- | ----- | ------ | -------- |
|     |         |       |        |          |
|     |         |       |        |          |
|     |         |       |        |          |
