---
title: "Асинхронное взаимодействие"
description: "Описание асинхронного взаимодействия"
version: 1
additional:
    team: ""
    author: ""
    service : ""
    maintainer: ""
    developer: ""
    status: "in_work"
    subscribers: [""]
draft: false
slug: ""
weight: 3
---

Документ содержит общее описание принципов асинхронного взаимодействия.


Есть 2 ас.взаимодействия:

1. Отправка сообщений от Centrifugo в APP Core по WSS:JSON
2. Чтение событий из kafka по kafka protokol