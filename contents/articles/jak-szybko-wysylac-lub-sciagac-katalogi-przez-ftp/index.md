---
title: Szybki download/upload katalogów poprzez FTP
date: 2014-02-26 11:59:54 
author: Wojciech Lubicz-Łapiński
template: article.jade
tags: shell, programowanie, linux, ftp
---

Najszybszą metodą przesyłania i ściągania całej gałęzi katalogów poprzez FTP, używając poleceń z konsoli, jest wykorzystanie programu [lftp](http://lftp.yar.ru "lftp") .

*lftp* jest rozbudowanym programem do transmisji plików, który obsługuje protokoły takie jak ftp/s, http/s, hftp, fish, sftp i torrent. Warto ten program zainstalować, gdyż może być wielce pomocny w niektórych sytuacjach.

Poniżej przykład wysyłania zawartości lokalnego katalogu *'local_dir'* do zdalnego *'remote_dir'* na serwerze *'hostname'*:

```bash
$ lftp -u user,password -e "mirror -R local_dir /remote_dir;quit" ftp://hostname
Total: 1 directory, 3 files, 0 symlinks
New: 3 files, 0 symlinks
20071573 bytes transferred in 162 seconds (121.8K/s)
```


Żeby zobaczyć zawartość zdalnego katalogu *'remote_dir'* na serwerze *'hostname'* wykonujemy polecenie:

```bash
$ lftp -u user,password -e "ls /remote_dir;quit" ftp://hostname
total 19612
-rw-r--r--  1 nobody  nogroup  15568717 Feb 25 23:29 eGroup.zip
-rw-r--r--  1 nobody  nogroup    113942 Feb 25 23:29 eGroup-pear.zip
-rw-r--r--  1 nobody  nogroup   4388914 Feb 25 23:30 wordpress.zip
```


Dla ściągnięcia zawartości zdalnego katalogu *'remote_dir'* z serwera *'hostname'* na katalog lokalny *'local_dir'* wykonujemy polecenie:

```bash
$ lftp -u user,password -e "mirror /remote_dir local_dir;quit" ftp://hostname
Total: 1 directory, 3 files, 0 symlinks
New: 3 files, 0 symlinks
20071573 bytes transferred in 20 seconds (981.0K/s)
```


To tylko najbardziej użyteczne przykłady korzystania z programu [lftp](http://lftp.yar.ru "lftp"). Warto dokładnie przejrzeć manual na stronie producenta i zapoznać się z szeregiem innych ciekawych opcji (jak np. możliwość równoległego wysyłania i ściągania plików).