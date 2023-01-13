---
title: Скачать видео с новостного сайта
lang: ru
description: Мой успешный опыт закачки видео с новостного сайта
tags: linux fishshell shell lifehacks
categories: ru
layout: post
---

## Шаг 1. Осматриваемся

Видео-плеер на сайте отображался в отдельном фрейме, я открыл HTML код этого фрейма.
В нём кода было немного и мне сразу бросилась в глаза строчка в коде на JavaScript:

```js
player.src([{"src":"https:\/\/video.inmedis.ru\/hls\/361559_c2f7a1dc0385e4be41ae95c74c990428\/master.m3u8","type":"application\/x-mpegURL"}]);
```

Посмотрел содержимое этого файла <span style="display:inline-block;overflow-x: auto">`https://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/master.m3u8`</span>:

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=4527940,RESOLUTION=1920x1080,FRAME-RATE=25.000,CODECS="avc1.640028,mp4a.40.2"
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/index-f1-v1-a1.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=2061917,RESOLUTION=1280x720,FRAME-RATE=25.000,CODECS="avc1.64001f,mp4a.40.2"
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/index-f2-v1-a1.m3u8

#EXT-X-I-FRAME-STREAM-INF:BANDWIDTH=164722,RESOLUTION=1920x1080,CODECS="avc1.640028",URI="http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/iframes-f1-v1-a1.m3u8"
#EXT-X-I-FRAME-STREAM-INF:BANDWIDTH=101294,RESOLUTION=1280x720,CODECS="avc1.64001f",URI="http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/iframes-f2-v1-a1.m3u8"
```

Затем содержимое этого файла <span style="display:inline-block;overflow-x: auto">`http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/index-f1-v1-a1.m3u8`</span>:

```
#EXTM3U
#EXT-X-TARGETDURATION:10
#EXT-X-ALLOW-CACHE:YES
#EXT-X-PLAYLIST-TYPE:VOD
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:1
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-1-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-2-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-3-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-4-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-5-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-6-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-7-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-8-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-9-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-10-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-11-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-12-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-13-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-14-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-15-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-16-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-17-f1-v1-a1.ts
#EXTINF:10.000,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-18-f1-v1-a1.ts
#EXTINF:7.093,
http://video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-19-f1-v1-a1.ts
#EXT-X-ENDLIST
```

## Шаг 2. Скачиваем фрагменты 

Скачал все файлики в текущую папку с именами содержащими лишь номер файла, одной командой для [FishShell](https://fishshell.com/): 

```bash
for n in (seq 19)
    http -o $n.ts -d video.inmedis.ru/hls/361559_c2f7a1dc0385e4be41ae95c74c990428/seg-$n-f1-v1-a1.ts
end
```

## Шаг 3. Склеиваем фрагменты в один файл 

Создал файл `frames.txt` со списком этих файлов в формате удобном для `ffmpeg`:

```bash
for x in (seq 19)
    echo file \'$x.ts\' >> frames.txt
end
```

И наконец склеил все скачаные фрагменты в один файл `news.ts`:

```bash
ffmpeg -f concat -safe 0 -i frames.txt -c copy news.ts
```
