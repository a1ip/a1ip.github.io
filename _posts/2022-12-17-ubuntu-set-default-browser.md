---
title: Изменить браузер по умолчанию в Ubuntu
lang: ru
description: сделать Google Chrome браузером по умолчанию в Ubuntu
tags: linux
categories: ru
layout: post
---

У меня долго не получалось изменить браузер по умолчанию. Помогли следующие команды:

```bash
xdg-mime default google-chrome.desktop text/html
xdg-mime default google-chrome.desktop x-scheme-handler/http
xdg-mime default google-chrome.desktop x-scheme-handler/https
xdg-mime default google-chrome.desktop x-scheme-handler/about
```

Можно проверить установленные значения так:

```bash
xdg-mime query default text/html
xdg-mime query default x-scheme-handler/http
xdg-mime query default x-scheme-handler/https
xdg-mime query default x-scheme-handler/about
```
