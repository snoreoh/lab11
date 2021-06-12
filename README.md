## Laboratory work XI

Данная лабораторная работа посвещена изучению процесса создания сеансов совместной разработки с использованием инструмента **ngrok**

1. Что такое?
**ngrok** exposes local servers behind NATs and firewalls to the public internet over secure tunnels.
**ngrok** предоставляет доступ к локальным серверам за NATS и брандмауэрами в Интернет по защищенным туннелям.
2. Как работает?
Первое - нужно загрузить и запустить программу на своем компьютере и предоставить ей порт сетевой службы, обычно веб-сервера.
Второе - подключиться к облачной службе ngrok, которая принимает трафик по общедоступному адресу.
Третье - трафик передается через процесс ngrok, запущенный на компьютере, а затем на указанный локальный адрес.

```sh
$ open https://ngrok.com/
```

## Tasks

- [x] 1. Ознакомиться со ссылками учебного материала
- [x] 2. Выполнить инструкцию учебного материала
- [x] 3. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial
1. переходим в корневой каталог
2. Создаем директорию 
3. Создаем директорию 
4. Задаем локальную переменную HOME_PREFIX
5. Выведем значение этой переменной
6. Задаем локальную перменную USERNAME

```sh
$ cd ~
$ mkdir install
$ mkdir tmp
$ export HOME_PREFIX=`pwd`/install
$ echo $HOME_PREFIX
$ export USERNAME=`whoami`
```
7. Переходим в директорию tmp
```sh
$ cd tmp
```
8. Скачиваем архив с библиотекой libevent, чтобы взаимодействовать с Libevent API 
9. Распаковываем архив и выводим его содержимое
10. Переходим в требуемую директорию с библиотекой
11. Указываем директорию, в которую будет производится установка
12. Производим установку
13. Поднимаемся на директорию выше

```sh
$ wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz
$ tar -xvzf libevent-2.1.8-stable.tar.gz
$ cd libevent-2.1.8-stable
$ ./configure --prefix=${HOME_PREFIX}
$ make && make install
$ cd ..
```
14. Скачиваем архив с библиотекой ncures, чтобы иметь возможность управлять вводом выводом на терминал. Она позволяет не беспокоиться об аппаратных различиях терминалов и писать переносимый код.
15. Распаковываем архив и выводим его содержимое
16. Переходим в требуемую директорию с библиотекой
17. Указываем директорию, в которую будет производится установка
18. Производим установку
19. Поднимаемся на директорию выше

```sh
$ wget http://invisible-island.net/datafiles/release/ncurses.tar.gz
$ tar -xvzf ncurses.tar.gz
$ cd ncurses-5.9
$ ./configure --prefix=${HOME_PREFIX}
$ make && make install
$ cd ..
```
20. Действия аналогичный предыдущим. Устанавливаем tmux.
tmux — свободная консольная утилита-мультиплексор, предоставляющая пользователю доступ к нескольким терминалам в рамках одного экрана.

```sh
$ wget https://github.com/tmux/tmux/releases/download/2.5/tmux-2.5.tar.gz
$ tar -xvzf tmux-2.5.tar.gz
$ cd tmux-2.5
$ ./configure --prefix=${HOME_PREFIX} CFLAGS="-I${HOME_PREFIX}/include -I${HOME_PREFIX}/include/ncurses" LDFLAGS="-L${HOME_PREFIX}/lib"
$ make && make install
$ cd ..
```
21. Скачиваем архив, содержащий ngrok
22. Установим unzip
23. Распаковываем скачаный архив
24. Перемещаем каталог с ngrok в директорию bin (полный путь: /Users/navckin/install/bin)
```sh
$ wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip
$ unizp ngrok-stable-linux-amd64.zip
$ mv ngrok ${HOME_PREFIX}/bin
```
25. LD_LIBRARY_PATH -это предопределенная переменная среды в Linux/Unix, которая задает путь, по которому компоновщик должен искать при связывании динамических библиотек/общих библиотек.
26. Задаем перемнные окружения 
27. Запускаем tmux

```sh
$ export LD_LIBRARY_PATH=${HOME_PREFIX}/lib
$ export PATH="${HOME_PREFIX}/bin:${PATH}"
$ tmux
```
28.  Возвращяемся в корневой каталог
29. Удаляем директории tmp и install

```sh
$ cd ~
$ rm -rf tmp install
```
30. Альтернативный способ установки tmux и ngrok
```sh
$ brew install tmux ngrok # or use linuxbrew 🎉
```
31. Создаем новую сессию
```sh
$ tmux new -s session_with_group
```
32. Теперь необходимо поднять вм, которую создавали в прошлой лабораторной
33. Открываем сайт и регистрируемся
34. задаем значению переменной значение токена
35. Указываем токен в качестве аутентификационного токена
36. Указываем порт, чтобы получить доступ по SSH

```sh
# Alisa:
$ open https://ngrok.com/signup
$ export NGROK_TOKEN=<токен>
$ ngrok authtoken ${NGROK_TOKEN}
$ ngrok tcp 22
<порт_ngrok_сервера>
```
37. Работаем в виртуальной машине
38.  Подключемся к созданной групповой сессии
39. Вертикальное разделение консольного окна
 
```sh
# Bob:
$ ssh ${USERNAME}@0.tcp.ngrok.io -p<порт_ngrok_сервера>
<пароль_от_учетной_записи>
$ tmux a -t session_with_group
$ <C-B>"
```

## Links

- [Tmux](https://raw.githubusercontent.com/tmux/tmux/master/README)
- [Libevent](http://libevent.org)
- [Ncurses](http://invisible-island.net/ncurses/)

Copyright (c) 2015-2021 The ISC Authors
