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

## Микрофон в bluetooth гарнитуре

Чтобы заработал микрофон в bluetooth гарнитуре, я зашёл в настройки `pulseaudio`, можно командой:

```bash
pavucontrol-qt
```

И во вкладке `Конфигурация` в профиле мне пришлось выбрать `Handsfree Head Unit (HFP)` вместо `High Fidelity Playback (A2DP Sink)` и тогда микрофон заработал!

## Распаковка архивов с именами файлов и директорий в иных кодировках

Если вы видите кракозябры, то это проблема текущей версии `p7zip`, которую использует графическая оболочка.
Если же использовать утилиту `unzip` из командной строки, то проблем нет.

Так, же хорошо с этим справляется утилита [`unar`](https://theunarchiver.com/command-line):

```bash
sudo apt install unar
```

Запускается из командной строки.

## Увеличение шрифта в адресной строке браузеров на движке Chromium

Сперва

```bash
cp /usr/share/applications/google-chrome.desktop ~/.local/share/applications
cp /var/lib/snapd/desktop/applications/brave_brave.desktop ~/.local/share/applications
```

В скопированных файлах нужно добавить в параметры запуска `--force-device-scale-factor=1.6`.
Так что теперь у меня в файле `~/.local/share/applications/google-chrome.desktop`:

```
Exec=/usr/bin/google-chrome-stable --force-device-scale-factor=1.6 %U
```

## Изменить браузер по умолчанию

У меня долго не получалось изменить браузер по умолчанию. Помогли следующие команды:

```bash
update-alternatives --config x-www-browser
update-alternatives --config gnome-www-browser
```

Возможно нужно было ещё выполнить и ниследующие (но без вышеукзанных, точно не заработало):

```bash
xdg-mime default google-chrome.desktop text/html
xdg-mime default google-chrome.desktop x-scheme-handler/http
xdg-mime default google-chrome.desktop x-scheme-handler/https
xdg-mime default google-chrome.desktop x-scheme-handler/about
```

А для Brave браузера установленного из snap

```bash
xdg-mime default brave_brave.desktop text/html
xdg-mime default brave_brave.desktop x-scheme-handler/http
xdg-mime default brave_brave.desktop x-scheme-handler/https
xdg-mime default brave_brave.desktop x-scheme-handler/about
```

Можно проверить установленные значения так:

```bash
xdg-mime query default text/html
xdg-mime query default x-scheme-handler/http
xdg-mime query default x-scheme-handler/https
xdg-mime query default x-scheme-handler/about
```

В файле `~/.config/mimeapps.list` в `Default Applications` и `Added Associations` должно быть прописано `brave_brave.desktop`.

А вместо файлов `~/.local/share/mimeapps.list` `~/.local/share/applications/mimeapps.list` у меня ссылки на файл `~/.config/mimeapps.list`.

```bash
ln -s ~/.config/mimeapps.list ~/.local/share/mimeapps.list
ln -s ~/.config/mimeapps.list ~/.local/share/applications/mimeapps.list
```

## Не отображаются Unicode Emoji

Проблема решилась установкой шрифтов в систему. А каких именно шрифтов — не знаю, возможно:

```bash
sudo apt install fonts-recommended
```
