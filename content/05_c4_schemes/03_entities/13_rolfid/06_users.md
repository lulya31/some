---
title: "Пользаватели (Users)"
description: "Описание агрегата Users"
slug: ""
version: 1
weight: 6
titleIcon: ""
draft: false
additional:
    author: "Полина Иванова"
    maintainer: "Сергей Панасюк"
    status: "in_work"
---

**Пользователи (агрегат)** - хранит в себе все данные о пользователях Flora. Пользователем Flora может являться как сотрудник Rolf, так и клиент. У сотрудников может быть установлен разный уровень доступа. 


{{<notice info>}}
[Описание переходов статусов, JSON представление сущности и атрибутивный состав](https://confluence.rlf-tech.com/pages/viewpage.action?pageId=11770142)
{{</notice>}}


## Типы пользователей
* Клиент
* Сотрудник Rolf


## Уровень доступа сотрудников Rolf
* Подчиненный
* Начальник


## Пользователи содержат
* Физическое лицо (person)
* Связь с ДЦ и ФГ (user_group_dealership)
* Телефоны (telephones)
* Электронная почта (emails)
* Документы (documents)
* HR данные (rolf_hr) - только для сотрудников Rolf
* Начальник (manager) - только для сотрудников Rolf
* Подчиненные (under_employees) - только для сотрудников Rolf

