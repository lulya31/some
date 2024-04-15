---
title: "Поиск"
description: "Страница поиска"
weight: 11
draft: false
slug: ""
titleIcon: "fa-solid fa-magnifying-glass"
---

<link href="/pagefind/pagefind-ui.css" rel="stylesheet">
<script src="/pagefind/pagefind-ui.js"></script>
<div id="searchPageFind"></div>
<script>
    window.addEventListener('DOMContentLoaded', (event) => {
        new PagefindUI({ element: "#searchPageFind", showSubResults: true });
    });
</script>
