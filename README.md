## Тестовое задание
Создать обновляемый репозиторий для ubuntu bionic

Исходные данные:
Проект https://github.com/peervpn/peervpn

- задача:
собрать проект из исходников для ubuntu bionic
запаковать полученный бинарный исполняемый файл в deb пакет, файл должен устанавливаться в /usr/local/bin/
опубликовать deb пакет в http репозитории (gpg шифрование не требуется)

- ожидаемый результат:
набор скриптов (программ, ansible плейбуков, т.п.) который позволяет собрать и запаковать бинарный файл в deb пакет и выложить его в репозиторий для ubuntu bionic

- верификация результата:
полученный репозиторий подключается к ubuntu bionic и не выдаёт ошибок при вызове apt update (допускаются ошибки из-за отсутствия gpg подписи)
собранный deb пакет устанавливается из репозитория, бинарный файл размещается в /usr/local/bin

## Инструкции по запуску плейбуков
Запуск плейбука с тегами для сборки и выкладки собранного пакета в локальный репозиторий.
```
ansible-playbook play.yml --tags build
```
Запуск плейбука для тестирования установки приложения согласно постановке задания.
```
ansible-playbook play.yml --tags install
```

## Комментарии

 Исходный код проекта peervpn написан под использование библиотеки libssl версии 1.0, которая на данный уже устарела. Для успешной сборки пакета необходимо
 - либо делать fork проекта peervpn и дорабатывать код под использование libssl 1.1, как это сделано, например, в репозитории https://github.com/BugMaster510945/peervpn 
 - либо установить libssl версии 1.0
 
 В постановке задания говорится "собрать проект из исходников для ubuntu bionic", что скорее не подразумевает правку исходного кода, однако если бы необходимо было править исходный код, то дополнительно я бы добавил в него файл для запуска сервиса peervpn и типовой конфиг-файл peervpn.
 
 Дополнительные комментарии по написанной ansible-роли можно найти в ее README файле внутри директории peervpn-role.

## Допущения
 - Сервер с репозиторием deb пакетов - это тот же сервер на котором происходит сборка. Если бы использовался отдельный сервер для репозитория - то код немного бы отличался.
 - Apache2 web server исталлируется в ходе выполнения playbook-а и иммет дефолтные настройки, в том числе и дефолтный DocumentRoot: "/var/www/html", который частично задается внутри переменной "repo_base_path". Настройки firewall и selinux не затрагиваются.
 - Файлы, генерируемые в ходе выполнения playbook-а в директорию с репозиторием имеют маску "peervpn_*", которая учтена в gitignore файле
 
