---
title: Настройки Ubuntu
lang: ru
description: Записки себе на память, о решении проблем при настройке Ubuntu
tags: linux
categories: ru
layout: post
---

## Добавить возможность набирать символы юникода

Я добавил файл `~/.config/lxqt/session.conf ` в раздел `[Keyboard]` строку :

```
options=compose:rwin, grp_led:scroll, grp:alt_shift_toggle
```
Так что раздел стал выглядеть вот так:

```
[Keyboard]
beep=true
delay=500
interval=30
layout="us,ru"
model=pc105
numlock=true
options=compose:rwin, grp_led:scroll, grp:alt_shift_toggle
variant=","
```

Может быть можно прописать в автозапуск, если непонятно какие конфиги менять:

```
setxkbmap -layout "us,ru" -option "grp:alt_shift_toggle,compose:rwin" -variant ","
```

Важное замечание: если используется файл со своими комбинациями `~/.XCompose`, то он
отключает все комбинации по умолчанию, прописанные в файле `/usr/share/X11/locale/en_US.UTF-8/Compose`.

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

<https://losst.pro/ustanovka-shriftov-v-linux>

Нужно просто создать папку и поместить в неё файлы шрифтов, возможно даже во вложеных папках.

```bash
mkdir ~/.fonts
```
Следующая команда обновит кэш шрифтов системы:

```bash
fc-cache -f -v
```

## Делаем эмулятор терминала QTerminal прозрачным

<https://askubuntu.com/questions/1121400/lubuntu-18-10-qterminal-window-transparency-setting>

В настройках сессии LXQt нужно поставить галочку у пункта `Compton`

Тогда появятся новые настройки `Эффекты окна`

## Сменить командную оболочку при запуске QTerminal

В настройках сеанса параметр `TERM` установить

```bash
qterminal -e "fish --login"
```
## Добавляем Firefox Developer Edition

Всё по этому руководству:

<https://linuxcool.ru/ustanovka-firefox-developer-v-ubuntu-linux-mint-i-drugie/>
