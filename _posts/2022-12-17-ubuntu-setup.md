---
title: Настройки Ubuntu
lang: ru
description: Записки себе на память, о решении проблем при настройке Ubuntu
tags: linux
categories: ru
layout: post
---

## Добавить возможность набирать символы юникода

Я добавил файл `~/.xinitrc` содержащий одну строку:

```
setxkbmap -layout "us,ru" -option "grp:alt_shift_toggle,compose:rwin" -variant ","
```

## Изменить браузер по умолчанию

У меня долго не получалось изменить браузер по умолчанию. Помогли следующие команды:

```bash
sudo update-alternatives --config x-www-browser
sudo update-alternatives --config gnome-www-browser
```

Возможно нужно было ещё выполнить и ниследующие (но без вышеукзанных, точно не заработало):

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

## Установка шрифтов

https://losst.pro/ustanovka-shriftov-v-linux

Нужно просто создать папку и поместить в неё файлы шрифтов, возможно даже во вложеных папках.

```bash
mkdir ~/.fonts
```
Следующая команда обновит кэш шрифтов системы:

```bash
fc-cache -f -v
```

## Делаем эмулятор терминала QTerminal прозрачным

https://askubuntu.com/questions/1121400/lubuntu-18-10-qterminal-window-transparency-setting

В настройках сессии LXQt нужно поставить галочку у пункта `Compton`

Тогда появятся новые настройки `Эффекты окна`

## Сменить командную оболочку при запуске QTerminal

В настройках сеанса параметр `TERM` установить

```bash
qterminal -e "fish --login"
```
