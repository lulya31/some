# Документация к проекту

Документация доступна по ссылке: \
**https://doc-system-architecture-main.com-dev.int.rolfcorp.ru/**

## Установка ПО 

Для локального запуска и работы с документацией необходимо установить:

* **Git**
* **Hugo**
* **Asciidoc**

### Установка Git (Windows)

Ссылка на скачивание для Windows:

https://git-scm.com/downloads 

### Установка Git (Linux / MacOS)

https://git-scm.com/book/en/v2/Getting-Started-Installing-Git 

### Настройка пользователей и ключей

> Для работы с проектом необходимо получить доступ к репозиториям Gitlab:\
> https://gitlab.int.rolfcorp.ru/one-rolf/doc/core \
> https://gitlab.int.rolfcorp.ru/one-rolf/doc/hugocms

* Указать пользователя и email. \
Необходимо указывать реальные значения!

```bash
git config user.name
git config user.email
```

* Создать ssh-ключи

```bash
ssh-keygen -t rsa -b 4096
```

* Выполнить импорт ключей в **Gitlab**.

### Установка Hugo

Установка по ссылке:

https://gohugo.io/getting-started/installing/

### Установка Asciidoc

Выполнить установку в следующем порядке:

* https://www.ruby-lang.org/en/documentation/installation/
* https://github.com/jirutka/asciidoctor-html5s
* https://docs.asciidoctor.org/pdf-converter/latest/install/
* https://docs.asciidoctor.org/diagram-extension/latest/
* https://docs.asciidoctor.org/asciidoctor/latest/syntax-highlighting/pygments/

### Node.js

Для работы поиска по статьям необходимо установить [NodeJS 16+](https://nodejs.org).

## Загрузка и работа с проектом

### Загрузка проекта

```bash
git clone --recurse-submodules git@gitlab.int.rolfcorp.ru:one-rolf/doc/core.git
```

### Просмотр документации локально

После скачивания проекта необходимо перейти в склонированную папку.

#### Linux / MacOS

Выполнить в терминале в папке проекта:

```shell
$ hugo server
```

#### Windows

1. Скопировать файл hugo.exe в директорию проекта
2. Выполнить в терминале в директории проекта:

```
./hugo.exe server
```

Документация доступна по адресу по умолчанию: http://localhost:1313/

### Созданине ветки

Перед началом работы требуется создать локальную ветку, где будут проводиться все изменения проекта:

```bash
git checkout -b story/JIRA_NUM
```

> `JIRA_NUM` - номер задачи в Jira, например CRM-815

### Обновление проекта

В случае, если необходимо обновить документацию из репозитория, следует это сделать с помощью процедуры `rebase main`

```bash
git checkout main
git fetch
git pull
git checkout story/JIRA_NUM
git rebase main
```

### Обновление под-модуля

Если под-модуль с темой был обновлен, то его следует также обновить локально:

```bash
git submodule update --remote 
```

### Применение изменений

После окончания работы (или при окончании одного из этапов) следует сохранить изменения:

```bash
git add .
git commit -m "What was done"
git push origin story/JIRA_NUM
```

Далее требуется создать _Merge Request_ в Gitlab и дождаться одобрения от владельца репозитория.

> **Запрещено** делать commit/push в ветку main!

## Работа с контентом

Общие правила:

- Текст в шапке устанавливается в файле `config.toml` на 5-й строке в параметре `title`
- Разделы документа находятся в директории `content` \
В данном разделе требуется размещать `.md` или `.adoc` файлы согласно сущестующим директориям и правилам (см. ниже)
- Все файлы и картинки сохраняются в папку `static`
    - Все изображения в папке Static раскладываются по папкам, которые именуются по схеме: \
        _<номер раздела>_<номер подраздела>_img_\
        Если подраздел отсутствует, то указывается <номер раздела>_<00>_img
- Все названия папок и файлов - _только латиница в нижнем регистре без пробелов_. \
Эти названия отображаются в адресной строке браузера, кириллица будет выглядеть нечитабельно и громоздко. Также будет удобнее делать перекрестные ссылки.

### Оформлению статей и файлов

- Если в метаданных статьи есть поле `slug`, то оно должно быть написано только латиницей, через **_ или -** если слов несколько и в нижнем регистре.
- Если же поля `slug` нет, то данное правило переходит на название самого .md-файла.
- Для корневых статей (_index.md) поле `slug` должно быть обязательно и иметь значение пустой строки ("")
- Поле `title` (заголовок) в метаданных статьи должно быть обязательно и должно быть взято в двойные кавычки ("")
- Поле `description` также указывается в двойных кавычках и должно содержать краткое описание статьи (необязательное поле)
- Каждой странице проставляется параметр `weight` (порядковый номер страницы), желательно (но не обязательно) соответствующий порядковому номеру в названии файла. \
    Чем больше значение `weight`, тем ниже по списку находится файл.
- Вначале имени папки/файла указывается _порядковый номер_ в двухзначном (если файлов много - трехзначном) формате.\
    Это нужно для ориентации в структуре папок, а еще удобно для связи текстовых фалов с файлами изображений.
- Для документа доступен _поиск_. \
    Поиск будет доступен, только если соблюдены все требования к файлам и папкам.

Пример корректного отображения файла для корневой статьи:

```
---
title: "Раздел тестов"
description: "Раздел посвящен"
slug: ""
weight
---
```

#### Генерация индексов

<span style="color: red">Перед началом, убедитесь, что соблюдены все требования к контенту и к среде</span>

Для генерации индексов статей для поиска необходимо выполнить скрипт `generate-indexes.sh`. \
Он находится в директории шаблона и требует npm, который идёт вместе с [NodeJS](https://nodejs.org).

Действия:

1. В терминале, находясь в корневой директории проекта hugo, пройдите в директорию шаблона `./themes/template/`:

```shell
cd themes/templates
```

2. Установите зависимые пакеты с помощью команды и дождитесь окончания установки:

```shell
npm install
```

3. Запустите скрипт для индексации статей:

```shell
sh generate-indexes.sh
```


### Требования к содержанию статей

Для стандартизации подходов к разработке документации необходимо придерживаться следующих правил ведения документации:

- Вся документация должна быть оформлена в _инкерментальном стиле_, то есть должны описываться не изменения, а то, как должен работать тот или функционал.
- _Содержание страницы_ будет добавлено по умолчанию, если количество слов превышает 400.
- Текстовые файлы должны быть _целостными, лаконичными и предметными_. \
Не рекомендуется создание общих файлов большого размера, содержащих информацию разного значения.
- Все постановки и требования следует писать _в отведенных для этого разделах_.
- Следует использовать _ссылки_ внутри документации, стараясь максимально избегать повторных требований/описаний.

## Полезные ссылки

Основные ссылки по рекомендуемым инструментам:

* Hugo: https://gohugo.io/
* Markdown: https://www.markdownguide.org/basic-syntax/
* Asciidoc: https://docs.asciidoctor.org/
* Asciidoc: writers guide: https://asciidoctor.org/docs/asciidoc-writers-guide/
* Asciidoctor-diagram installation: https://docs.asciidoctor.org/diagram-extension/latest/
* Asciidoctor-PDF installation: https://docs.asciidoctor.org/pdf-converter/latest/install/
* Pygments: https://pygments.org/download/
* Mermaid installation: https://mermaid.js.org/intro/#installation
* Mermaid: https://mermaid.live/
* GitLab OneRolf: https://gitlab.int.rolfcorp.ru/one-rolf/doc
* Команды GIT: https://git-scm.com/book/en/v2
* VS Code: https://code.visualstudio.com/
* Mardown tables: https://www.tablesgenerator.com/markdown_tables
