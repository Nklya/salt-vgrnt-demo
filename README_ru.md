# SaltStack demo with Vagrant and GitFS

[In English](README.md)

Inspired and based on https://github.com/UtahDave/salt-vagrant-demo

## Описание

!!! Этот пример использует готовые ключи, в случае использования этого примера в production окружении, ключи нужно сменить. Версия 2018.3.0

### Как солт работает с окружениями

Если мы хотим использовать изолированные окружения, то нужно:

* Настроить конфиг мастера (указать в нем репозитории для корня, формул и пилларов)
* При необходимости настроить права доступа к репозиторию. [Ссылка](https://www.youtube.com/watch?v=RaeKLKaqPoo)
* В конфигах миньонов должны быть прописаны параметры имени окружения и указание, что пиллары также в окружении. Параметры `saltenv` и `pillarenv_from_saltenv`.

## Как работает настройка [GitFS](https://docs.saltstack.com/en/latest/topics/tutorials/gitfs.html)

Видео на эту тему: [1](https://www.youtube.com/watch?v=0VFKRExZotM), [2](https://www.youtube.com/watch?v=RaeKLKaqPoo), [3](https://www.youtube.com/watch?v=ZVAUfAiP6qo)

В общем и целом, для работы gitfs необходима установленная питоновская библиотека для работы с гитом. По умолчанию используется pygit2, но в Debian и Ubuntu она не умеет работать с https. Другая библиотека - GitPython, и она в Ubuntu работает.
Для закрытых реп можно использовать ssh ключи и прописывать паблик в деплой ключи например. Либо вбивать логин-пароль.

Pillar в gitfs настраиваются по-другому, [ссылка](https://docs.saltstack.com/en/latest/ref/pillar/all/salt.pillar.git_pillar.html)

## Как запустить

* Установить вагрант
* При необходимости поменять пути к репозиториям с конфигами
* В папке выполнить `vagrant up`

## Полезные команды

* `salt-call --versions-report` - отчет по версиям
* `salt '*' grains.ls` - просмотр какие факты есть
* `salt '*' grains.items` - просмотр собранных фактов
* `salt '*' pillar.ls` - показать какие пилары есть
* `salt '*' pillar.items` - показать пилары
* `salt '*' state.show_top` - просмотр top файлов
* `salt-run fileserver.update` - обновление файлов, подгрузка изменений из гита при необходимости.
* `salt-run fileserver.file_list` - показать список файлов, дополнительно можно указать окружение, например `saltenv=prod`
* `salt-run fileserver.dir_list` - показать список папок
* `salt-run fileserver.envs`
* `salt-run git_pillar.update` - обновить пилары из гита
* `salt-run pillar.show_pillar`
* `salt-run pillar.show_top`
* `salt-run saltutil.sync_pillar` - синхронизировать пилары с мастера на миньоны. Можно указать `_all`, и тогда засинхронизируется все.
