# Домашнее задание к занятию 1 «Введение в Ansible»

## Подготовка к выполнению

1. Установите Ansible версии 2.10 или выше.
2. Создайте свой публичный репозиторий на GitHub с произвольным именем.
3. Скачайте [Playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.

## Основная часть

1. Попробуйте запустить playbook на окружении из `test.yml`, зафиксируйте значение, которое имеет факт `some_fact` для указанного хоста при выполнении playbook.

----

```bash
$ ansible-playbook -i ./playbook/inventory/test.yml ./playbook/site.yml
```
скрин
![Screenshot1_1](https://github.com/megasts/05-virt-04-docker-in-practice/blob/main/img/Screenshot1_1.png)

----

2. Найдите файл с переменными (group_vars), в котором задаётся найденное в первом пункте значение, и поменяйте его на `all default fact`.

----

скрин
![Screenshot1_2](https://github.com/megasts/05-virt-04-docker-in-practice/blob/main/img/Screenshot1_2.png)

![Screenshot1_3](https://github.com/megasts/05-virt-04-docker-in-practice/blob/main/img/Screenshot1_2.png)

----

3. Воспользуйтесь подготовленным (используется `docker`) или создайте собственное окружение для проведения дальнейших испытаний.

скрин

4. Проведите запуск playbook на окружении из `prod.yml`. Зафиксируйте полученные значения `some_fact` для каждого из `managed host`.

скрин

5. Добавьте факты в `group_vars` каждой из групп хостов так, чтобы для `some_fact` получились значения: для `deb` — `deb default fact`, для `el` — `el default fact`.
6.  Повторите запуск playbook на окружении `prod.yml`. Убедитесь, что выдаются корректные значения для всех хостов.

скрин

7. При помощи `ansible-vault` зашифруйте факты в `group_vars/deb` и `group_vars/el` с паролем `netology`.

```bash
$ ansible-vault encrypt ./playbook/group_vars/deb/examp.yml 

$ ansible-vault encrypt ./playbook/group_vars/el/examp.yml
```

скрин

8. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь в работоспособности.

скрин

9. Посмотрите при помощи `ansible-doc` список плагинов для подключения. Выберите подходящий для работы на `control node`.

ansible.builtin.local

скрин

10. В `prod.yml` добавьте новую группу хостов с именем  `local`, в ней разместите localhost с необходимым типом подключения.

```yml
local:
    hosts:
      localhost:
         ansible_connection: local
```

11. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь, что факты `some_fact` для каждого из хостов определены из верных `group_vars`.

скрин

12. Заполните `README.md` ответами на вопросы. Сделайте `git push` в ветку `master`. В ответе отправьте ссылку на ваш открытый репозиторий с изменённым `playbook` и заполненным `README.md`.

13. Предоставьте скриншоты результатов запуска команд.

## Необязательная часть

1. При помощи `ansible-vault` расшифруйте все зашифрованные файлы с переменными.

скрин

2. Зашифруйте отдельное значение `PaSSw0rd` для переменной `some_fact` паролем `netology`. Добавьте полученное значение в `group_vars/all/exmp.yml`.

скрин

3. Запустите `playbook`, убедитесь, что для нужных хостов применился новый `fact`.

скрин

4. Добавьте новую группу хостов `fedora`, самостоятельно придумайте для неё переменную. В качестве образа можно использовать [этот вариант](https://hub.docker.com/r/pycontribs/fedora).

скрин

5. Напишите скрипт на bash: автоматизируйте поднятие необходимых контейнеров, запуск ansible-playbook и остановку контейнеров.

```bash
#!/bin/bash

docker run -d --rm --name fedora pycontribs/fedora sleep 60
docker run -d --rm --name ubuntu pycontribs/ubuntu:latest sleep 60
docker run -d --rm --name centos7 pycontribs/centos:7 sleep 60
ansible-playbook -i ~/Projects/mnt-homeworks/08-ansible-01-base/playbook/inventory/prod.yml ~/Projects/mnt-homeworks/08-ansible-01-base/playbook/site.yml --ask-vault-pass
```

6. Все изменения должны быть зафиксированы и отправлены в ваш личный репозиторий.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---
